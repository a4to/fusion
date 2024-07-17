
# Fusion

Fusion is a Go-based utility that simplifies the process of embedding project directories and executing a main script within a temporary environment. It is particularly useful for creating standalone executables that bundle all necessary scripts and files, allowing for easy distribution and execution without external dependencies.

## Features

- **Embed project files**: Automatically embed all files from a specified directory.
- **Compile into a single executable**: Compiles giant directories and all project dependencies into a single, binary executable.
- **Runtime execution**: Supports executing the main script using various runtimes (e.g., bash, node, python).
- **Temporary environment**: Runs the main script in a secure, temporary environment, cleaning up after execution.
- **Automatic runtime detection**: Determines the appropriate runtime for the main script based on file extension.

## Usage

### Command Line Flags

- `-main`: Path to the main executable script (required).
- `-dir`: Path to the project directory containing files to be embedded (required).
- `-name`: Name of the final executable (default: "app").
- `-runtime`: Runtime to execute the main script (e.g., bash, node, python). If not provided, Fusion attempts to determine the runtime based on the file extension.

### Example

Assuming you have a bash script `run.sh` and a project directory `myproject`, you can create a standalone executable as follows:

```sh
fusion -main run.sh -dir myproject -name myapp
```

This command creates an executable named `myapp`, which embeds the contents of `myproject` and runs `run.sh` using the appropriate runtime.

## How It Works

1. **Embed Files**: Fusion reads all files from the specified project directory and embeds them using Go's `embed` package.
2. **Generate Main Script**: It generates a Go source file (`main.go`) that extracts the embedded files to a temporary directory and executes the main script using the specified or determined runtime.
3. **Build Executable**: The Go source file is compiled into a standalone executable, embedding all necessary files and logic.

## Example Structure

```plaintext
.
├── fusion
├── myproject
│   ├── script1.sh
│   └── config.json
└── run.sh
```

After running `fusion -main run.sh -dir myproject -name myapp`, you get an executable `myapp` that contains `run.sh` and all files within `myproject`.


