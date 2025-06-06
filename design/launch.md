# Shotgun App Launch Guide

This guide provides instructions on how to set up your environment and run the Shotgun App.

## 1. Prerequisites

Before you begin, ensure you have the following installed on your system:

-   **Go**: Version 1.20 or newer. (Check with `go version`)
    -   Installation: [https://golang.org/doc/install](https://golang.org/doc/install)
-   **Node.js and npm**: Node.js (which includes npm) LTS version. (Check with `node -v` and `npm -v`)
    -   Installation: [https://nodejs.org/](https://nodejs.org/)
-   **Wails CLI**: The Wails command-line tool.
    -   Installation (after Go is set up):
        ```bash
        go install github.com/wailsapp/wails/v2/cmd/wails@latest
        ```
    -   Verify installation: `wails doctor` (This command helps check if your system is ready for Wails development).

## 2. Project Setup

1.  **Copy Files**: Copy all the provided project files (`main.go`, `app.go`, `go.mod`, `wails.json`, the `frontend/` directory, and this `design/` directory) into a new directory on your computer. Let's call this new directory `shotgun-app`.

    ```
    shotgun-app/
    ├── go.mod
    ├── main.go
    ├── app.go
    ├── wails.json
    ├── frontend/
    │   ├── package.json
    │   ├── vite.config.js
    │   ├── index.html
    │   ├── src/
    │   │   ├── main.js
    │   │   ├── App.vue
    │   │   ├── components/
    │   │   │   └── FileTree.vue
    │   │   └── assets/
    │   │       └── main.css
    │   └── wailsjs/  (This will be generated by Wails)
    └── design/
        ├── architecture.md
        └── launch.md
    ```

2.  **Navigate to Project Directory**:
    Open your terminal or command prompt and change to the project's root directory:
    ```bash
    cd path/to/shotgun-app
    ```

3.  **Install Go Dependencies**:
    Wails should handle this, but you can also run:
    ```bash
    go mod tidy
    ```

4.  **Install Frontend Dependencies**:
    Navigate to the `frontend` directory and install npm packages:
    ```bash
    cd frontend
    npm install
    cd .. 
    ```
    (Then return to the project root directory)

## 3. Running the Application (Development Mode)

With Wails, you can run the application in development mode, which provides live reloading for frontend changes.

1.  **Run `wails dev`**:
    In the root directory of the project (`shotgun-app/`), run:
    ```bash
    wails dev
    ```
    This command will:
    -   Build the Go backend.
    -   Start the Vite development server for the frontend.
    -   Open the application window.

    Any changes you make to the Go code will require restarting `wails dev`. Changes to Vue components or other frontend assets should trigger a live reload of the frontend.

## 4. Building the Application (Production)

To create a distributable, standalone application:

1.  **Run `wails build`**:
    In the root directory of the project (`shotgun-app/`):
    ```bash
    wails build
    ```
    This command will:
    -   Build the frontend assets for production.
    -   Compile the Go backend.
    -   Bundle them together into an executable file (e.g., `.exe` on Windows, `.app` on macOS, or a binary on Linux).
    -   The output will be in a `build/bin/` directory within your project.

    You can also build for specific platforms using flags (e.g., `wails build -platform windows/amd64`). Refer to the Wails documentation for more details on cross-compilation.

## 5. Troubleshooting

-   **`wails command not found`**: Ensure that your Go `bin` directory (usually `$GOPATH/bin` or `$HOME/go/bin`) is in your system's `PATH` environment variable.
-   **`wails doctor`**: Run this command to check for common setup issues. It provides guidance on resolving them.
-   **Frontend Build Issues**: Check the console output from `npm install` or `wails dev` for any errors related to Node.js, npm, or Vite.
-   **Go Build Issues**: Check the console output for Go compilation errors. Ensure your Go version is compatible.

Refer to the official Wails documentation for more detailed information: [https://wails.io](https://wails.io)