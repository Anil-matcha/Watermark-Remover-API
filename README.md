# Watermark Remover API

Remove supported overlays from video using the general-purpose and Seedance-tuned endpoints. Check model-specific input schemas and price on the landing page before choosing a route.

[Muapi Watermark Remover API landing page](https://muapi.ai/watermark-remover) · [API reference](https://muapi.ai/docs/api-reference) · [Playground](https://muapi.ai/playground) · [Create an API key](https://muapi.ai/access-keys)

## Related Projects

- [Background-Remover-API](https://github.com/Anil-matcha/Background-Remover-API)
- [AI-Video-Editing-API](https://github.com/Anil-matcha/AI-Video-Editing-API)

## What this API covers

Use the endpoint that matches the task and input media. The routes below are enabled Muapi model IDs checked against the current model catalog; availability, request fields, and pricing can change, so verify the linked landing page and endpoint schema before production use.

| Endpoint | Purpose | Category |
|---|---|---|
| `video-watermark-remover` | Watermark Remover | `Video to Video` |
| `seedance-2-watermark-remover` | Watermark Remover | `Video to Video` |
| `seedance-2-video-watermark-remover-pro` | Watermark Remover Pro | `Video to Video` |

## Quick start

Muapi uses an asynchronous REST contract. Submit a JSON request with your API key, save the returned `request_id`, then poll the result endpoint. Replace sample URLs with files you control and fields with values supported by the selected endpoint.

```bash
curl -X POST https://api.muapi.ai/api/v1/video-watermark-remover \
  -H "Content-Type: application/json" \
  -H "x-api-key: $MUAPI_API_KEY" \
  -d '{
    "video_url": "https://example.com/replace-with-your-file"
  }'
```

### Request fields in this example

| Field | Requirement | Notes |
|---|---|---|
| `video_url` | Required | URL of the input video. |

### Poll for the result

```bash
curl "https://api.muapi.ai/api/v1/predictions/$REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_API_KEY"
```

Poll until the task status is `completed` or `failed`. Read the response’s output URLs on completion; download outputs you need to retain, since provider-hosted URLs may expire.

## Choosing an endpoint

Compare supported inputs and output behavior first, then resolution, duration, quality controls, latency, and price for your use case. Similar names do not guarantee interchangeable request schemas. This repository lists representative routes; the canonical landing page contains the current task-specific explanation, examples, and pricing context.

## Errors and production notes

- Keep the API key in an environment variable; do not commit credentials.
- Validate inputs against the selected endpoint’s current schema.
- Handle non-success HTTP responses and failed task states explicitly.
- Retry only when appropriate for the error; avoid submitting duplicate billable jobs after a timeout without checking the original `request_id`.
- Confirm current pricing and availability on the Muapi page before estimating production cost.
