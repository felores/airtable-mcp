# Airtable MCP Server
[![smithery badge](https://smithery.ai/badge/airtable-server)](https://smithery.ai/server/airtable-server)

A Model Context Protocol server that provides tools for interacting with Airtable's API. This server enables programmatic management of Airtable bases, tables, fields, and records through Claude Desktop or other MCP clients.

This MCP server features a specialized implementation that allows it to build tables in stages, leveraging Claude's agentic capabilities and minimizing the failure rate typically seen in other MCP servers for Airtable when building complex tables. It also includes [system prompt](https://github.com/felores/airtable-mcp/blob/main/prompts/system-prompt.md) and [project knowledge](https://github.com/felores/airtable-mcp/blob/main/prompts/project-knowledge.md) markdown files to provide additional guidance for the LLM when leveraging projects in Claude Desktop.

## Requirements: Node.js

1. Install Node.js (version 18 or higher) and npm from [nodejs.org](https://nodejs.org/)
2. Verify installation:
   ```bash
   node --version
   npm --version
   ```

⚠️ **Important**: Before running, make sure to setup your Airtable API key

## Obtaining an Airtable API Key

1. Log in to your Airtable account at [airtable.com](https://airtable.com)
2. Create a personal access token at [Airtable's Builder Hub](https://airtable.com/create/tokens)
3. In the Personal access token section select these scopes: 
     - data.records:read
     - data.records:write
     - schema.bases:read
     - schema.bases:write
4. Select the workspace or bases you want to give access to the personal access token
5. Keep this key secure - you'll need it for configuration

## Installation

### Installing via Smithery

To install Airtable MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/airtable-server):

```bash
npx -y @smithery/cli install airtable-server --client claude
```

### Method 1: Using npx (Recommended)
1. Navigate to the Claude configuration directory:

   - Windows: `C:\Users\NAME\AppData\Roaming\Claude`
   - macOS: `~/Library/Application Support/Claude/`
   
   You can also find these directories inside the Claude Desktop app: Claude Desktop > Settings > Developer > Edit Config

2. Create or edit `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "airtable": {
      "command": "npx",
      "args": ["@felores/airtable-mcp-server"],
      "env": {
        "AIRTABLE_API_KEY": "your_api_key_here"
      }
    }
  }
}
```
Note: For Windows paths, use double backslashes (\\) or forward slashes (/).

### Method 2: Using mcp-installer:
mcp-installer is a MCP server to install other MCP servers.
1. Install [mcp-installer](https://github.com/anaisbetts/mcp-installer)
2. Install the Airtable MCP server by prompting Claude Desktop:
```bash
Install @felores/airtable-mcp-server set the environment variable AIRTABLE_API_KEY to 'your_api_key'
```
Claude will install the server, modify the configuration file and set the environment variable AIRTABLE_API_KEY to your Airtable API key.

### Method 3: Local Development Installation
If you want to contribute or modify the code run this in your terminal:
```bash
# Clone the repository
git clone https://github.com/felores/airtable-mcp.git
cd airtable-mcp

# Install dependencies
npm install

# Build the server
npm run build

# Run locally
node build/index.js
```
Then modify the Claude Desktop configuration file to use the local installation:
```json
{
  "mcpServers": {
    "airtable": {
      "command": "node",
      "args": ["path/to/airtable-mcp/build/index.js"],
      "env": {
        "AIRTABLE_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

### Verifying Installation

1. Start Claude Desktop
2. The Airtable MCP server should be listed in the "Connected MCP Servers" section
3. Test with a simple command:
```
List all bases
```

## Features

### Available Operations

#### Base Management
- `list_bases`: List all accessible Airtable bases
- `list_tables`: List all tables in a base
- `create_table`: Create a new table with fields
- `update_table`: Update a table's name or description

#### Field Management
- `create_field`: Add a new field to a table
- `update_field`: Modify an existing field

#### Record Operations
- `list_records`: Retrieve records from a table
- `create_record`: Add a new record
- `update_record`: Modify an existing record
- `delete_record`: Remove a record
- `search_records`: Find records matching criteria
- `get_record`: Get a single record by its ID

### Field Types
- `singleLineText`: Single line text field
- `multilineText`: Multi-line text area
- `email`: Email address field
- `phoneNumber`: Phone number field
- `number`: Numeric field with optional precision
- `currency`: Money field with currency symbol
- `date`: Date field with format options
- `singleSelect`: Single choice from options
- `multiSelect`: Multiple choices from options

### Field Colors
Available colors for select fields:
- `blueBright`, `redBright`, `greenBright`
- `yellowBright`, `purpleBright`, `pinkBright`
- `grayBright`, `cyanBright`, `orangeBright`
- `blueDark1`, `greenDark1`

## Contributing

We welcome contributions to improve the Airtable MCP server! Here's how you can contribute:

1. Fork the Repository
   - Visit https://github.com/felores/airtable-mcp
   - Click the "Fork" button in the top right
   - Clone your fork locally:
     ```bash
     git clone https://github.com/your-username/airtable-mcp.git
     ```

2. Create a Feature Branch
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Make Your Changes
   - Follow the existing code style
   - Add tests if applicable
   - Update documentation as needed

4. Commit Your Changes
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```

5. Push to Your Fork
   ```bash
   git push origin feature/your-feature-name
   ```

6. Create a Pull Request
   - Go to your fork on GitHub
   - Click "New Pull Request"
   - Select your feature branch
   - Describe your changes in detail

### Development Guidelines

- Use TypeScript for new code
- Follow semantic commit messages
- Update documentation for new features
- Add examples for new functionality
- Test your changes thoroughly

### Getting Help

- Open an issue for bugs or feature requests
- Join discussions in existing issues
- Ask questions in pull requests

Your contributions help make this tool better for everyone. Whether it's:
- Adding new features
- Fixing bugs
- Improving documentation
- Suggesting enhancements

We appreciate your help in making the Airtable MCP server more powerful and user-friendly!

## License

[MIT](LICENSE)

---

Made with ❤️ by the Airtable MCP community
