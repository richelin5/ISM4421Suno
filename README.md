# ISM4421Suno — Suno Studio

A single-page AI music generator built on the [Suno API](https://docs.sunoapi.org). It's one static `index.html`, with no build step, no backend, and no dependencies.

## Features
- **Simple mode**: describe a song, pick a genre, and generate (2 variations per request).
- **Custom mode**: title, style, your own lyrics, excluded styles, vocal gender, length (10s–6min), variety, and optional style/weirdness/audio weights.
- **AI lyrics writer**: turn a short theme into structured lyrics.
- **Model picker**: V6 (default), V6 Wild, V6 Mini.
- **Library**: live status, early streaming, in-page player, cover art, lyrics, download, copy link, reuse settings. Saved in the browser, and it resumes polling after a refresh.
- **Extend**: continue any finished track from a chosen timestamp.
- **Credits** balance in the header.

## API key
Each user clicks **Add API key** and pastes their own key from <https://sunoapi.org/api-key>.
The app checks the key against the credits endpoint, keeps it only in that browser's `localStorage`,
and sends it only to `api.sunoapi.org`. No key is stored in this repository.

## Deploy to Netlify
1. In Netlify, choose **Add new site → Import an existing project** and pick this repo, branch `main`.
2. Leave the build command empty. The publish directory is `.` (already set in `netlify.toml`).
3. Deploy. Or drag-and-drop the folder into Netlify Drop.

To run it locally, open `index.html` or run `npx serve .`.

## API endpoints used
| Action | Endpoint |
| --- | --- |
| Generate | `POST /api/v1/generate` |
| Poll status | `GET /api/v1/generate/record-info?taskId=` |
| Extend | `POST /api/v1/generate/extend` |
| Lyrics | `POST /api/v1/lyrics` + `GET /api/v1/lyrics/record-info` |
| Credits | `GET /api/v1/generate/credit` |

The API requires a `callBackUrl`. The app sends a placeholder and gets results by polling instead.
Generated files are kept by the API for about 14 days.
