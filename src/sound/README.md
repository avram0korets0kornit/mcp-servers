# Windows Sound MCP Server

A Model Context Protocol server that provides the ability to play Windows system sounds. This server enables LLMs to list available system sounds and play them by name, with cross-platform support.

### Available Tools

- `list_sounds` - List all available Windows system sounds in the configured directory.
  - No required arguments

- `play_sound` - Play a specific Windows system sound by name.
  - Required arguments:
    - `sound_name` (string): Name of the sound file to play (including the extension)

## Installation

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/), no specific installation is needed. You can use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-play-windows-sound*.

### Using PIP

Alternatively, you can install `mcp-play-windows-sound` via pip:

```bash
pip install mcp-play-windows-sound
```

After installation, you can run it as a script using:

```bash
python -m mcp_play_windows_sound
```

## Configuration

### Configure for Claude.app

Add to your Claude settings:

<details>
<summary>Using uvx</summary>

```json
{
  "mcpServers": {
    "windows-sound": {
      "command": "uvx",
      "args": ["mcp-play-windows-sound"]
    }
  }
}
```
</details>

<details>
<summary>Using pip installation</summary>

```json
{
  "mcpServers": {
    "windows-sound": {
      "command": "python",
      "args": ["-m", "mcp_play_windows_sound"]
    }
  }
}
```
</details>

### Configure for VS Code

For manual installation, add the following JSON block to your User Settings (JSON) file in VS Code. You can do this by pressing `Ctrl + Shift + P` and typing `Preferences: Open User Settings (JSON)`.

Optionally, you can add it to a file called `.vscode/mcp.json` in your workspace. This will allow you to share the configuration with others.

> Note that the `mcp` key is needed when using the `mcp.json` file.

<details>
<summary>Using uvx</summary>

```json
{
  "mcp": {
    "servers": {
      "windows-sound": {
        "command": "uvx",
        "args": ["mcp-play-windows-sound"]
      }
    }
  }
}
```
</details>

<details>
<summary>Using pip installation</summary>

```json
{
  "mcp": {
    "servers": {
      "windows-sound": {
        "command": "python",
        "args": ["-m", "mcp_play_windows_sound"]
      }
    }
  }
}
```
</details>

### Customization - Sound Folder

By default, the server looks for sounds in the Windows Media folder (typically C:\Windows\Media). You can override this by adding the argument `--sound-folder` to the `args` list in the configuration.

Example:
```json
{
  "command": "python",
  "args": ["-m", "mcp_play_windows_sound", "--sound-folder=/path/to/custom/sounds"]
}
```

## Example Interactions

1. List all available sounds:
```json
{
  "name": "list_sounds",
  "arguments": {}
}
```
Response:
```json
{
  "sounds": ["chimes.wav", "chord.wav", "ding.wav", "notify.wav", "recycle.wav", "tada.wav", ...],
  "count": 10
}
```

2. Play a specific sound:
```json
{
  "name": "play_sound",
  "arguments": {
    "sound_name": "tada.wav"
  }
}
```
Response:
```json
{
  "sound_name": "tada.wav",
  "success": true,
  "message": "Successfully played sound: tada.wav"
}
```

## Cross-Platform Support

While designed primarily for Windows, this server also works on:

- **macOS**: Uses `afplay` to play sound files
- **Linux**: Uses `aplay` or `paplay` to play sound files

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```bash
npx @modelcontextprotocol/inspector uvx mcp-play-windows-sound
```

Or if you've installed the package in a specific directory or are developing on it:

```bash
cd path/to/servers/src/sound
npx @modelcontextprotocol/inspector uv run mcp-play-windows-sound
```

## Examples of Prompts for Claude

1. "List all available Windows sounds"
2. "Play the Windows notification sound"
3. "What Windows system sounds are available?"
4. "Play the 'tada.wav' sound"

## License

mcp-play-windows-sound is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License.