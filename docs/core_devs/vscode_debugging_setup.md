# VS Code - Setting up for Debugging

Setting up Visual Studio Code (VSCode) for debugging the 0L framework involves a few steps. In our case we want to debug a package that we have not setup for debugging. Here's a general guide to get you started:

### 1. Install Prerequisites
- **Rust**: Ensure Rust is installed on your system. You can install it from [the Rust website](https://www.rust-lang.org/).
- **Visual Studio Code**: If not already installed, download and install VSCode from [the VSCode website](https://code.visualstudio.com/).

### 2. Install VSCode Extensions
- Open VSCode and install the following extensions:
  - **Rust (rls)**: This is the official Rust extension for VSCode, which provides features like auto-completion, code formatting, and linting.
  - **CodeLLDB or C/C++**: These extensions provide debugger support. CodeLLDB is often recommended for Rust debugging.

### 3. Configure the Project
- Open your Rust project (`libra-framework`) in VSCode.
- There's a `.vscode` folder with access to all the packages

### Note: If There Was Not a Configuration, Set Up the Debug Configuration
- Go to the Run and Debug view in VSCode (usually the play icon on the sidebar).
- Click on "create a launch.json file".
- Select "Rust" as the environment.
- This will create a `launch.json` file in the `.vscode` directory. You may need to modify this file based on your project's needs. A basic configuration for a Rust project might look like this:

  ```json
    {
      "name": "your config",
      "type": "lldb",
      "request": "launch",
      "cargo": {
        "args": [
          "build",
          "-p",   // Replace with the correct package name if `rescue` is part of a specific package
          "rescue" // Replace with the correct binary name if different
        ],
      },
      "args": [], // Add any necessary command-line arguments for the rescue tool here
      "cwd": "${workspaceFolder}",
      "preLaunchTask": "", // Optional: A VSCode task to run before launching the debugger
      "postDebugTask": "" // Optional: A VSCode task to run after the debugging session ends
    },
  ```
  Replace `my_project` with the name of your binary.
  
### 4. In Our Case We Will Need to Add a Configuration to Include a Package for Rescue.

- Edit `.vscode/launch.json` and add
```
    {
        "name": "rescue tool",
        "type": "lldb",
        "request": "launch",
        "cargo": {
          "args": [
            "build",
            "-p",   
            "rescue" 
          ],
        },
        "args": [], 
        "cwd": "${workspaceFolder}",
        "preLaunchTask": "", 
        "postDebugTask": "" 
    }
```

### 5. Start Debugging
- Once your `launch.json` is set up, you can start debugging by selecting the appropriate configuration(`rescue tool`) from the Run and Debug dropdown and clicking the green play button.

### 6. Set Breakpoints
- Click to the left of the line numbers in your code editor to set breakpoints.
- When the debugger runs, execution will pause at these points, allowing you to inspect variables, step through code, etc.

### 7. Additional Debugging Features
- Use the Debug Console in VSCode to run commands, evaluate expressions, or inspect variables during a debugging session.
- You can also use the watch window to keep an eye on specific variables.

### Notes:
- The debugging experience can vary based on the project's complexity and the specific Rust environment.
- If you encounter issues, check the Rust extension's output and the developer console in VSCode for error messages.
