---
name: ai-rap-video
description: Use when someone wants an AI rap video, rap name, or short rap lyrics. Use AI Rap Generators MCP for name and lyric tools, and create and poll an original duo video when the user provides two public photo URLs and has enough credits.
---

# AI Rap Video

## When to use

Use this skill for rap names, short English rap drafts, birthday lyrics, or an original 15-second duo rap video. The remote AI Rap Generators MCP server provides text tools and video task tools. Video rendering costs 10 account credits per task.

## Workflow

1. Identify whether the user wants a name, lyric draft, or finished video.
2. For names, use `generate_rap_names` or `generate_wu_tang_name`. For a general verse, use `generate_rap_lyrics` with a topic up to 300 characters and an optional supported style. For a birthday verse, use `generate_birthday_rap_lyrics` with a name, personal detail, and supported relationship.
3. If the user wants a video, first call `get_credits`. Explain that one video costs 10 credits; do not promise a free first render. Continue only when the account can cover the cost and the user wants to spend those credits.
4. The MCP video tool requires exactly two publicly accessible HTTPS image URLs. It cannot upload chat attachments or private/local files. Ask the user to provide URLs they control and can share with the video provider, or direct them to the [website generator](https://airapgenerators.com/) for private uploads.
5. Use `list_rap_stages` to choose a supported stage when needed. Call `create_rap_video` with the two image URLs and optional stage, occasion, and creative direction. Only use images the user is authorized to use; people shown must be consenting adults. Do not submit a generation request unless the user asked to create the video.
6. Return the task ID and explain that rendering is asynchronous. Poll `get_video_status` no more than once every three seconds until it returns `success` or `failed`. Share `videoUrl` only when the task succeeds. Failed renders return the reserved credits.
7. Present generated names and lyrics as suggestions. A video may adapt its generated verse and does not promise to use a separate lyric draft word for word.

## Tool and input notes

- `generate_rap_names`: up to 12 suggestions; `mustInclude` is limited to 12 characters.
- `generate_wu_tang_name`: one inspired name and a short interpretation.
- `generate_rap_lyrics`: a short original English verse from a topic up to 300 characters.
- `generate_birthday_rap_lyrics`: a name (up to 40 characters), personal detail (up to 200), and relationship (`best-friend`, `couple`, `family`, `coworker`, or `kid-friendly`).
- `create_rap_video`: exactly two public HTTPS image URLs; optional stage, occasion, and creative direction up to 500 characters. Creates a 15-second vertical duo video for 10 credits.
- `get_video_status`: checks a task created by the same account. Wait at least three seconds between status requests.
- `get_credits`: reports the current balance and whether one video can be created.
- `list_rap_stages`: lists the available stage IDs and render details.

The current API creates original duo videos. It does not accept image uploads, create solo videos, or make meme remakes. Do not imitate a named artist or reproduce existing lyrics.

## Access and limits

The remote MCP endpoint is `https://airapgenerators.com/api/mcp`. Tool calls require an AI Rap Generators account API key sent as a Bearer token. Create or revoke keys in [Settings → API Keys](https://airapgenerators.com/settings/apikeys). The two name tools are free. General and birthday lyric drafts share 10 free drafts per account per 24-hour period. Video tasks cost 10 credits; check `get_credits` because a free first video is not guaranteed.

## Links

- [Product and video generator](https://airapgenerators.com/)
- [MCP setup and tool reference](https://airapgenerators.com/mcp)
- [Raw skill landing page](https://airapgenerators.com/ai-rap-video-skill)
- [REST API reference](https://airapgenerators.com/api)
- [Claude setup](https://airapgenerators.com/integrations/claude)
- [Cursor setup](https://airapgenerators.com/integrations/cursor)
- [Codex setup](https://airapgenerators.com/integrations/codex)
- [Pricing and free allowances](https://airapgenerators.com/pricing)
