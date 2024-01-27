# ghūl programming language examples

This repository contains examples of the ghūl programming language. 

## prerequisites

To use the examples project you need either [GitHub Codespaces](https://github.com/features/codespaces) or [Visual Studio Code](https://code.visualstudio.com/)

## opening the examples project

### GitHub Codespace

To open the examples in a GitHub Codespace in your browser or in VS Code Desktop:
- open this repo in GitHub
- make sure you're on the `<> Code` tab
- click the `Code` link at the top right corner of the page
- click the `+` icon to create a new Codespace on the `main` branch
- wait for a few moments while GitHub sets up the Codespace
- when VSCode opens in your browser either:
  - continue to use the examples directly in the browser
  - click on the rectangle in the bottom left of the page labelled 'Codespaces'
  - select `Open in VS Code Desktop` from the menu that pops up

### devcontainer

To open the examples in a devcontainer in VS Code Desktop using Docker:
- ensure you have Docker installed and working
- clone this repository to your development machine
- open the project folder in Visual Studio Code 
- either:
  - click the `Reopen in Container` button, when it pops up in the bottom right of the window, OR
  - press `Ctrl` + `Shift` + `P` and then select `Dev Containers: Reopen in Container` 

### open in VSCode locally
To open the examples directly in your local VSCode development environment:

- ensure you have the [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) installed and on the PATH
- clone this repository to your local machine
- open the cloned project folder in Visual Studio Code

### check the language extension is running

Make sure the [ghūl Visual Studio Code language extension](https://marketplace.visualstudio.com/items?itemName=degory.ghul) is installed and running: if you open any `.ghul` source file, the code should be highlighted, and you should see definition information when you hover the cursor over symbols.

If you're using VSCode Desktop and the extension is not running, either install it from the [marketplace](https://marketplace.visualstudio.com/items?itemName=degory.ghul) or install it using the extensions view (click on the extensions icon to the left of the Activity Bar, and then enter 'degory ghul' in the search box)

If you're using a Codespace in your browser and the extension is not running, try deleting and recreating the codespace.

## using the examples

## getting around the project
The project consists of:
- this document
- the MIT license
- the root MSBuild project file `examples.ghulproj`
- `Directory.Build.props`, which contains package references for some standard ghūl libraries
- config folders for VSCode and the development container
- folders for the various examples

### viewing and editing an example
You can drill down into the different example folders to view and edit the code.

Try browsing to `hello-world.ghul` by either expanding the `hello-world` folder in the Project Explorer view and then clicking on the `hello-world.ghul` source file, or by searching for it with `<ctrl>` + `P` and typing `hello-world`.

### running an example
To run an example:
- open a terminal 
- `cd` into that example's folder
- `dotnet run`

Run the hello-world example:
```sh
# cd into the example folder:
cd hello-world

# run the example project
dotnet run
```

Expected output:
```plaintext
Hello, World!
```

Alternatively, there are VSCode build tasks configured to run each of the examples. Open the build task list with `<ctrl>` + `<shift>` + `B`

### editing an example

Open `hello-world.ghul` again and change the text that's being written to the console to something different:

```ghul
entry() =>
    IO.Std.write_line("This is some different text");
```

Then re-run the hello-world example, and verify you see the updated text:
```sh
# cd into the example folder:
cd hello-world

# run the example project
dotnet run
```

Expected output:
```plaintext
This is some different text
```

### opening an individual example project

Each individual example folder contains a .NET project. You can open these project folders separately in VSCode or in a Codespace in your browser. You don't need to do this just to view the examples, tinker with the code, and to run them. You might want to open a project folder directly in VSCode if you choose to use it as a starting point for a new project. The [ghūl .NET templates](https://www.nuget.org/packages/ghul.templates) or the [ghūl GitHub repo template](https://github.com/degory/ghul-repository-template) might be better options for this however.

Note that some of the configuration for these projects is being inherited from the root folder of the repo, so if you move a project folder out from under project repo root, you will need to copy this shared config into the example project folder (`Directory.Build.props`, `.config` and `.devcontainer`).

### using a different devcontainer image

The project is configured to use the [ghūl development container image](https://github.com/degory/ghul/pkgs/container/ghul%2Fdevcontainer). You can use a different container image if you prefer - just edit the configuration in the `.devcontainer` folder accordingly. Make sure the image you select includes the .NET 8.0 SDK, with `dotnet` on the PATH.

## language extension features
The ghūl language extension for Visual Studio Code provides a few features that make working on ghūl projects easier, including:

- syntax highlighting
- error highlighting as you type
- code snippets for various language constructs
- symbol information on hover
- intelligent code completion
- function signature help
- find uses
- go to/peek definition
- go to/peek references
- go to/peek implementations
- go to symbol in file
- go to symbol in workspace
- inteligent symbol rename

## contributing

Feel free to contribute new ghūl language examples by raising a PR.

## issues and feedback

I want to ensure that this examples project is as low friction and as useful as possible. If you have any problems at all using it, please [open an issue in the GitHub repo](https://github.com/degory/ghul-examples/issues/new/choose) and I'll do my best to help.
