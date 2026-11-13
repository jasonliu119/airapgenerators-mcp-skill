# AI Rap Generators MCP and Skill

[AI Rap Generators](https://airapgenerators.com/?ref=github) provides a hosted MCP server for creating 15-second rap videos from two public HTTPS image URLs, checking tasks and credits, and generating rap names and short lyric drafts. Video generation costs 10 account credits per task; an account API key is required. See the [MCP guide](https://airapgenerators.com/mcp) and [pricing](https://airapgenerators.com/pricing).

## Connect

Use the remote Streamable HTTP endpoint `https://airapgenerators.com/api/mcp` with `Authorization: Bearer <API_KEY>`. Create an API key in [account settings](https://airapgenerators.com/settings/apikeys). Clients requiring stdio can use the published `airapgenerators-mcp` npm bridge:

```json
{"mcpServers":{"airap":{"command":"npx","args":["-y","airapgenerators-mcp"],"env":{"AIRAP_API_KEY":"<your-api-key>"}}}}
```

## Install the skill

```sh
npx skills add jasonliu119/airapgenerators-mcp-skill
```

The skill describes how to select the tools, check credits before creating a video, and poll for results. It does not upload local files. Use images you have permission to share.

Tools: `create_rap_video`, `get_video_status`, `get_credits`, `list_rap_stages`, `generate_rap_names`, `generate_wu_tang_name`, `generate_rap_lyrics`, and `generate_birthday_rap_lyrics`.
