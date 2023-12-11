# HistoryExplorerChatGPTPlugin

An interactive plugin that uses SK and GPT to create personalised, immersive journeys through different historical eras, complete with interactive dialogues and historical trivia.

This project contains the code for a ChatGPT plugin. It includes the following components:

- An endpoint that serves up an ai-plugin.json file for ChatGPT to discover the plugin
- A generator that automatically converts prompts into semantic function endpoints
- The ability to add additional native functions as endpoints to the plugin

## Prerequisites

- [.NET 6](https://dotnet.microsoft.com/download/dotnet/6.0) is required to run this project.
- [Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) is required to run this project.
- Install the recommended extensions
  - [C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
  - [Semantic Kernel Tools](https://marketplace.visualstudio.com/items?itemName=ms-semantic-kernel.semantic-kernel)

## Configuring the project

To configure the project, you need to provide the following information:

- Define the properties of the plugin in the [appsettings.json](./azure-function/appsettings.json) file.
- Enter the API key for your AI endpoint in the [local.settings.json](./azure-function/local.settings.json) file.

### Using appsettings.json

Configure an OpenAI endpoint

1. Copy [settings.json.openai-example](./config/appsettings.json.openai-example) to `./appsettings.json`
2. Edit the `kernel` object to add your OpenAI endpoint configuration
3. Edit the `aiPlugin` object to define the properties that get exposed in the ai-plugin.json file

Configure an Azure OpenAI endpoint

1. Copy [settings.json.azure-example](./config/appsettings.json.azure-example) to `./appsettings.json`
2. Edit the `kernel` object to add your Azure OpenAI endpoint configuration
3. Edit the `aiPlugin` object to define the properties that get exposed in the ai-plugin.json file

### Using local.settings.json

1. Edit the `Values` object to add your OpenAI endpoint configuration in the `apiKey` property

## Running the project

To run the Azure Functions application just hit `F5`.

To build and run the Azure Functions application from a terminal use the following commands:

```powershell
cd azure-function
dotnet build
cd bin/Debug/net6.0
func host start  
```

If you want to preview it in an actual ChatGPT-like experience, use [Chat CoPilot](https://github.com/microsoft/chat-copilot) and point it to the local endpoint at `http://localhost:7071/.well-known/ai-plugin.json` to add the plugin while this project is running.

## Technical information

This project makes use of whatever planner is the default for semantic skills in this type of project. Ideally it would make use of the new handlebars planner for generating multi-step plans, which uses Handlebars templates. This is instrumental in structuring historical narratives and interactions. For example, generating a story about a specific historical event or era. Unfortunately, with the release candidate releasing partway through the hackathon and a lack of documentation I was unable to work out how to switch to the new planner.

Likewise, an assistant persona could be created to make GPT respond more like an old storyteller or historian, but this was also not possible due to the lack of documentation. The plan was to utilize templated assistant instructions for dynamically creating stories based on the historical context and user inputs.

### Building the Time Travel Experience

Users can select time periods, ask questions, or interact with the narrative.

Interactive Narratives: Use GPT to create engaging dialogues and descriptions of historical events and figures.

Dynamic Story Creation: Employ Handlebars templates to structure the narratives dynamically, allowing for user choices to influence the story flow.
