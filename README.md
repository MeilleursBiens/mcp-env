# mcp-env
[![npm version](https://img.shields.io/npm/v/@c-delouvencourt/mcp-env.svg)](https://www.npmjs.com/package/@c-delouvencourt/mcp-env)
[![total downloads](https://img.shields.io/npm/dt/@c-delouvencourt/mcp-env.svg)](https://www.npmjs.com/package/@c-delouvencourt/mcp-env)

Use environment variables in your MCP server definitions.

> Fork of [envmcp](https://github.com/griffithsbs/envmcp) by Ben Griffiths.

## Quick Start

```bash
# Use default ~/.env.mcp file
npx @c-delouvencourt/mcp-env your-mcp-server $DATABASE_URL

# Specify custom env file
npx @c-delouvencourt/mcp-env --env-file .env your-mcp-server $API_KEY $DATABASE_URL

# Short flag version
npx @c-delouvencourt/mcp-env -e /path/to/secrets.env your-mcp-server $MY_SECRET
```

## Usage in MCP Clients

Prefix your server command with mcp-env.

_Before (secrets exposed in config)_: 
```json
{
  "my_database": {
    "command": "my-mcp-server",
    "args": ["postgresql://user:password@hostname/db"]
  }
}
```
_After (secrets in ~/.env.mcp)_:
```json
{
  "my_database": {
    "command": "npx",
    "args": ["@c-delouvencourt/mcp-env", "my-mcp-server", "$DATABASE_URL"]
  }
}
```

## How It Works

1. Looks for `.env.mcp` in current directory, then parent directories, finally `~/.env.mcp`
2. If `--env-file` is specified, uses that file instead
3. Loads environment variables from the file
4. Replaces `$VARIABLE_NAME` references in your command arguments
5. Executes the command with substituted values

## Installation

```bash
npm install -g @c-delouvencourt/mcp-env
```

## Options

- `--env-file <path>`, `-e <path>`: Specify custom environment file path

## Environment File Format

```
DATABASE_URL=postgresql://user:password@localhost/db
API_KEY=your-secret-api-key
# This is a comment
QUOTED_VALUE="value with spaces"
```

See `sample.env.mcp` for more examples.

## License

MIT 
