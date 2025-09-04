# Motoko MCP Server Template for ICP Ninja

Welcome! This template provides a complete, ready-to-deploy Motoko MCP server for the [Prometheus Protocol](https://github.com/prometheus-protocol/prometheus-protocol) ecosystem, adapted for the ICP Ninja online IDE.

No need to install anything on your machine to get started. Let's dive in.

Launch Now in ICP Ninja: https://icp.ninja/i?s=wOrZM

---

## The ICP Ninja Workflow

In this IDE, you don't use a terminal for deployment. Instead, you have two main buttons:

*   **`Run`**: Deploys your server to a **temporary** canister. This canister is free and perfect for testing, but it will be automatically destroyed after 45 minutes.
*   **`Publish`**: Deploys your server to a **permanent** canister that you control. To use this, you'll need to have an account with ICP and cycles to power your application.

---

## Part 1: Quick Start (Deploy in 60 Seconds)

This section will get your server live and testable in minutes.

### Step 1: Deploy a Temporary Server

Click the **`Run`** button in the ICP Ninja interface.

Wait for the deployment process to complete. You'll see the output in the console panel, which will include your new temporary canister ID.

### Step 2: Test with the MCP Inspector

Your server is now live with a couple default resources and a default `get_weather` tool. Let's test it.

1.  **Copy your Canister ID** from the deployment output panel.
2.  **Construct the Inspector URL:** Create a URL with this format:
    ```
    https://[YOUR_CANISTER_ID].icp0.io/mcp
    ```
3. **Run MCP Inspector**: From your terminal, run:
    ```bash
    npx @modelcontextprotocol/inspector
    ```
4.  **Open the URL**: The MCP Inspector will open a browser tab. Enter your URL to your MCP server in the box and click 'connect'. You can now list and fetch resources and tools, and invoke the `get_weather` tool (spoiler alert, its always sunny!).

🎉 **Congratulations!** You have a working MCP server running on the Internet Computer.

---

## Part 2: Unlocking Advanced Features (Local Development)

The ICP Ninja IDE is fantastic for quick deployments and testing. However, to unlock features like **monetization (OAuth)** and **publishing to the Prometheus App Store**, you'll need to download this project and work with it on your local machine.

Here's a brief overview of how that works.

### Prerequisites for Local Development

If you decide to download the code, you'll need these tools on your system:

1.  **DFX:** The DFINITY Canister SDK. [Installation Guide](https://dfinity.org/developers).
2.  **Node.js:** Version 18.0 or higher. [Download](https://nodejs.org/).
3.  **MOPS:** The Motoko Package Manager. [Installation Guide](https://mops.one/docs/install).

### Enabling Monetization 💰

Ready to add paid tools? The process involves enabling the Prometheus OAuth flow.

1.  **Activate Auth Code:** In `src/main.mo`, you'll uncomment the block of code that initializes the `authContext`.
2.  **Deploy Changes:** Run `dfx deploy` (or `npm run deploy`) from your local terminal.
3.  **Register with Auth Server:** Use a built-in script to register your server as a client with the Prometheus Auth Server.
    ```bash
    # This command is run locally, not in the IDE
    npm run auth register
    ```

### Publishing to the Prometheus App Store 🚀

To make your server discoverable, you can submit it for verification.

1.  **Initialize Manifest:** A command-line wizard helps you create a `prometheus.yml` manifest file.
    ```bash
    # Run locally
    npm run app-store init
    ```
2.  **Submit for Verification:** Once your manifest is complete (including a Git commit hash), you submit it for an audit.
    ```bash
    # Run locally
    npm run app-store submit
    ```
3.  **Publish WASM:** After a successful audit, you publish the final, verified code to the Prometheus Registry.
    ```bash
    # Run locally
    npm run app-store -- publish --app-version "0.1.0"
    ```

---

## What's Next?

-   **Customize Your Tool:** Open `src/main.mo` to see how the `echo` tool is built and start creating your own custom MCP tools.
-   **Learn More:** Check out the [Motoko MCP SDK documentation](https://github.com/prometheus-protocol/motoko-sdk) for advanced features.

Happy hacking!