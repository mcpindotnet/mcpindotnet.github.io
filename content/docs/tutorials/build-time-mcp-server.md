---
weight: 10001
date: "2025-08-10T05:33:22+01:00"
draft: false
author: "Ankit Sarkar"
title: "Build Time MCP Server using C# MCP SDK & NodaTime"
toc: true
description: "Learn how to use C# SDK to build MCP Server"
publishdate: "2025-08-07T05:33:22+01:00"
tags: ["Beginners"]
categories: [""]
keywords: [
  "Model Context Protocol .NET",
  "MCP C# SDK",
  "MCP server in C#",
  "MCP client .NET",
  "build MCP server C#",
  "MCP vs function calling",
  "OpenAI MCP support",
  "DeepMind MCP integration",
  "Copilot MCP",
  "MCP security vulnerabilities",
  "MCP vulnerabilities prompt injection",
  "MCP security audit",
  "latest MCP updates 2025",
  "MCP adoption OpenAI Google DeepMind",
  "how to build an MCP server in C#",
  "step by step MCP C# example",
  "MCP integration .NET Azure Copilot",
  "MCP .NET tutorial 2025",
  "how to create an MCP server in C#",
  "step-by-step guide to Model Context Protocol in .NET",
  "MCP with Semantic Kernel C# tutorial",
  "best way to integrate MCP with Blazor",
  "C# MCP plugin for AI agents",
  "build AI agents in C#",
  "Semantic Kernel agents .NET",
  "LangChain vs Semantic Kernel",
  "C# AI integration",
  "AI agent framework C#",
  "Blazor AI chatbot example",
  "MCP server example code",
  "C# OpenAI integration",
  "AI tools for .NET developers",
  "Vector database integration C#",
  "MCP API server with ASP.NET Core",
  "real-time AI agent communication in C#",
  "Model Context Protocol .NET",
  "MCP .NET",
  "MCP in C#",
  "Semantic Kernel MCP",
  "MCP server .NET",
  "MCP client .NET",
  "MCP for Blazor",
  "Model Context Protocol C# example",
  "MCP agent framework .NET",
  "OpenAI MCP .NET"
]
twitter:
  card: "summary"
  site: "@anktsrkr"
  creator: "@anktsrkr"
  title: "Build Time MCP Server using C# MCP SDK & NodaTime"
  description: "Learn how to use C# SDK to build MCP Server"
  image: ""
---
As we continue to explore the Model Context Protocol (MCP), we will now focus on how to build an MCP server using the C# SDK. This tutorial will guide you through the process of setting up a basic MCP server, which can be used to handle requests from MCP clients such as VS Code, LM Studio and others.

### What we are going to build?
In this tutorial, we will build a simple MCP server using the C# SDK and NodaTime for handling time-related operations. The server will be capable of processing requests from MCP clients and responding with the appropriate context information. Below are the few example queries that the server should be able to handle:

1. What time is it now? (will use system timezone)
2. What time is it in Tokyo?

To get started, ensure you have the following prerequisites:

1. **.NET SDK**: Make sure you have the .NET 10 SDK installed on your machine. You can download it from the [.NET website](https://dotnet.microsoft.com/en-us/download/dotnet/10.0). You can also use lower versions to build the server. Later we will deploy it as a NuGet package and to run it `dnx` is required, which is shipped as part of the .NET SDK, starting with version 10 preview 6.

2. **IDE**: Use an IDE like Visual Studio or Visual Studio Code for a better development experience.

Once you have the prerequisites in place, you can start building your MCP server. There are several ways to do this, as we are going to build `stdio` based server, we will simplify the process by using the console application.

### Step 1: Create a New Console Application
Open your terminal or command prompt and run the following command to create a new console application:

```bash
dotnet new console -n Dnx.TimeMcpServer
```
This command creates a new directory named `Dnx.TimeMcpServer` with a basic console application structure.

### Step 2: Add Required NuGet Packages
Next, navigate to the newly created project directory:

```bash
cd Dnx.TimeMcpServer
```

Now, add the required NuGet packages for building the MCP server:

```bash
dotnet add package ModelContextProtocol --prerelease
dotnet add package Microsoft.Extensions.Hosting
dotnet add package NodaTime
```
1. **ModelContextProtocol**: This package provides the core functionality for building MCP servers and clients. It includes the necessary abstractions and implementations for handling MCP requests and responses.

2. **Microsoft.Extensions.Hosting**: This package is used to create and manage the application's host, which is responsible for starting and stopping the server. It provides a simple way to configure services and middleware for the application.

3. **NodaTime**: This package is a date and time library for .NET that provides a more robust and flexible way to work with time zones and durations. It is essential for handling the time-related queries that our MCP server will process.

### Step 3: Define the Input and Output Records
Let's create a new file named `CurrentTimeInput.cs` in the project directory under `src/Models` folder.

```csharp
using System.ComponentModel;

public record CurrentTimeInput
{
    [Description("IANA timezone name (e.g., 'America/New_York', 'Europe/London'). If not provided, the system's default timezone is used.")]
    public string? Timezone { get; init; } = Environment.GetEnvironmentVariable("local-timezone") ?? default!;
}
```
The `CurrentTimeInput` record defines the input structure for the tool. It contains a single property, `Timezone`, which is a string representing the IANA timezone name. The property is initialized with the value of the `local-timezone` environment variable, if it exists, or defaults to `null`.

Next, create another file named `TimeResult.cs` in the same directory:

```csharp
using System.ComponentModel;

public record TimeResult
{
    [Description("The timezone in which the time is recorded.")]
    public required string Timezone { get; init; }
    
    [Description("The ISO 8601 formatted time string.")]
    public required string IsoTime { get; init; }

    [Description("A boolean indicating whether daylight saving time (DST) is currently in effect.")]
    public required bool IsDst { get; init; }
}
```
The `TimeResult` record defines the output structure for the tool. It contains three properties:

1. `Timezone`: A string representing the IANA timezone name.
2. `IsoTime`: A string representing the current date and time in ISO 8601 format.
3. `IsDst`: A boolean indicating whether the current time is in daylight saving time.

### Step 4: Define our first tool
Now that we have our initial setup complete, we need to define the tool. In this case, we will create a tool for handling time-related queries.

1. Create a new class file named `TimeTools.cs` in the project directory under `src/Tools` folder.

2. Define the `TimeTools` class as follows:

```csharp
using ModelContextProtocol;
using ModelContextProtocol.Server;
using NodaTime;
using NodaTime.Extensions;
using NodaTime.Text;
using System.ComponentModel;

public class TimeTools
{
    private static readonly LocalDateTimePattern _localDateTimePattern = LocalDateTimePattern.CreateWithInvariantCulture("yyyy'-'MM'-'dd'T'HH':'mm':'ss");

    [McpServerTool(Name = "get_current_date_time", UseStructuredContent = true), Description("Get current date and time in a specific timezone.")]
    public static TimeResult GetCurrentTime(CurrentTimeInput currentTimeInput)
    {
        var targetTimezone = currentTimeInput?.Timezone ?? DateTimeZoneProviders.Tzdb.GetSystemDefault().Id;

        try
        {
            var dateTimeZone = DateTimeZoneProviders.Tzdb[targetTimezone];
            var instant = SystemClock.Instance.GetCurrentInstant();
            var zonedDateTime = instant.InZone(dateTimeZone);

            return new TimeResult
            {
                Timezone = targetTimezone,
                IsoTime = _localDateTimePattern.Format(zonedDateTime.LocalDateTime),
                IsDst = zonedDateTime.IsDaylightSavingTime()
            };
        }
        catch (KeyNotFoundException)
        {
            throw new McpException($"Invalid timezone: {targetTimezone}");
        }
        catch (Exception)
        {
            throw new McpException($"Something went wrong, try again.");
        }
    }
}
```
In the above code, we use two attributes: `McpServerTool` and `Description`.

1. **McpServerTool**: This attribute is used to define a tool that can be invoked by the MCP server. It has few parameters but we will focus on only one parameter, leave the others as defaults and will discuss them later.

   - `Name`: This specifies the name of the tool, which is used to identify it in requests. In this case, it is set to `"get_current_date_time"`.
   - `UseStructuredContent`: This parameter indicates whether the tool should try to populate output schema information. In this case, it is set to `true`.

2. **Description**: This attribute provides a LLM-readable description of the tool's functionality. It is used to give LLMs more context about what the tool does and how to use it.

Together, these attributes help to define the behavior and purpose of the `GetCurrentTime` tool within the MCP server.

The `GetCurrentTime` method is a static method that handles requests for the current date and time in a specific timezone. It takes a `CurrentTimeInput` as a parameter. The method first retrieves the target timezone from the input or defaults to the system's timezone. It then uses the `NodaTime` library to get the current instant and convert it to the specified timezone. The result is returned as a `TimeResult` object, which includes the timezone, the ISO-formatted time, and whether the time is in daylight saving time.

The exception handling in the `GetCurrentTime` method is designed to catch and handle specific errors that may occur during the execution of the method. There are two main `catch` blocks:

1. **KeyNotFoundException**: This exception is thrown when the specified timezone is not found in the `DateTimeZoneProviders.Tzdb` collection. In this case, the method throws a `McpException` with a message indicating that the timezone is invalid.

2. **General Exception**: This catch block is a fallback for any other exceptions that may occur. It throws a `McpException` with a generic error message, prompting the user to try again.

By handling exceptions in this way, the method ensures that errors are communicated clearly to the caller, and it prevents unhandled exceptions from propagating further.

#### Why did we use `McpException`?
`McpException` is a custom exception type that is used to represent errors that occur within the MCP server tools. By using a specific exception type, we can provide more meaningful error messages and handle errors in a consistent way across different tools.

In the `GetCurrentTime` method, we use `McpException` to wrap and re-throw exceptions that occur during the execution of the method. This allows us to provide a clear error message to the caller, indicating what went wrong and how to fix it.

Using `McpException` also allows us to match with specification of error handling in the MCP server tools. For example, we can define specific error codes and messages for different types of errors, making it easier for clients to understand and handle errors in a consistent way.

### Step 5: Configure the MCP Server
Now that we have defined our tool, we need to configure the MCP server to use it. This involves updating `Program.cs` to set up the server and register the tool. 
  
Open the `Program.cs` file and replace its content with the following code:

```csharp
using Dnx.TimeMcpServer.Tools;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using System.Text.Json;
using System.Text.Json.Serialization.Metadata;

var builder = Host.CreateApplicationBuilder(args);

builder.Logging.AddConsole(o => o.LogToStandardErrorThreshold = LogLevel.Trace);

var jsonOptions = new JsonSerializerOptions
{
    TypeInfoResolver = new DefaultJsonTypeInfoResolver(),
    PropertyNamingPolicy = JsonNamingPolicy.SnakeCaseLower,
};

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithTools<TimeTools>(jsonOptions);

await builder.Build().RunAsync();
```

In the above code, we are configuring the MCP server to use the `TimeTools` class that we defined earlier. The `AddMcpServer` method sets up the MCP server, and the `WithStdioServerTransport` method configures it to use standard input/output for communication. The `WithTools<TimeTools>(jsonOptions)` method registers the `TimeTools` class as a tool that can be invoked by MCP clients. 

The `JsonSerializerOptions` object is used to configure the JSON serialization settings for the MCP tools. It specifies that the property names should be serialized in `snake_case` format, which is a common convention for tools.

### Step 6: Test the MCP Server
Now that we have configured the MCP server and registered our tool, we can now test the server to ensure it is working correctly. For this tutorial, we will use **MCP Inspector**, an interactive developer tool for testing and debugging MCP servers.

To test the MCP server using MCP Inspector, follow these steps:
1. **Install MCP Inspector**: If you haven't already, install it via the terminal with the following command:

```bash
npx @modelcontextprotocol/inspector
```
Once installed, it will automatically open a UI in your default web browser. You can use this UI to interact with your MCP server and send requests to it.

2. **Start the MCP Server**: In the UI of MCP Inspector, set the _Transport Type_ to `STDIO`, _Command_ as `dotnet` and _Arguments_ as `run --project "<path-to-your-project>"` and click on the "Connect". 

3. **Send a Test Request**: Once connected,  under **Tools** tab, click on **List Tools** to see the available tools and their details. Select the tool `get_current_date_time` and fill in the input field with the timezone you want to test. For example, you can enter `America/New_York` or leave it empty to use the system's default timezone. Click on **Run Tool** to send the request.

4. **View the Response**: After sending the request, you should see the response from the MCP server in the UI. This response will include the current date and time for the specified timezone, or an error message if something went wrong. You can use this information to verify that your MCP server is working correctly and returning the expected results.

5. **Validate the Response**: Since we defined `UseStructuredContent`, the UI will validate the response against the expected structure and display any errors or warnings if the response does not match the expected format. In our case, we expect the response __Valid according to output schema__.

### Step 7: Configure MCP Client
In this tutorial we will configure VS Code and LM Studio to work with the MCP server.

####  Configure VS Code
To configure Visual Studio Code to work with the MCP server, we just need to add a new server in our mcp.json file in your .vscode folder or your user settings:

```json
{
	"servers": {
		"dnx-time-server": {
			"type": "stdio",
			"command": "dotnet",
			"args": [
				"run",
				"--project",
				"<path-to-your-project>"
			]
		}
	},
	"inputs": []
}
```
When we go into GitHub Copilot and toggle on Agent mode, Let's ask the question "What is the current date and time in London?" 

<video width="640" height="480" controls>
  <source src="/videos/video1.mp4" type="video/mp4">
</video>

As we can see in the video, the response from the MCP server includes the current date and time in London, formatted according to the specified output schema.

#### Configure LM Studio
To configure LM Studio to work with the MCP server, we need to add a new server in the MCP settings.

```json
{
	"mcpServers": {
		"dnx-time-server": {
			"command": "dotnet",
			"args": [
				"run",
				"--project",
				"<path-to-your-project>"
			]
		}
	}
}
```

Let's ask the same question in LM Studio: "What is the current date and time in London?" 


<video width="640" height="480" controls>
  <source src="/videos/video2.mp4" type="video/mp4">
</video>

Same as VS Code, the response from the MCP server includes the current date and time in London, formatted according to the specified output schema.

### Conclusion
In this tutorial, we have successfully set up an MCP server and configured both Visual Studio Code and LM Studio to interact with it. We tested the server using MCP Inspector and verified that it responds correctly to requests for the current date and time in different time zones. This setup allows for efficient development and testing of applications that rely on the Model Context Protocol.

In the next tutorial, we will go even further and will learn how to deploy the MCP server to nuget and docker!
