# VisualAI Studio — AI-Powered Poster Creator

A local, responsive React and Express app for the full practical-exam workflow: campaign brief, three prompt variations, image concepts, manual comparison, editable poster composition, and a print-ready report. Demo artwork is generated locally as labeled SVG illustrations; it is never presented as AI-generated. Add a backend API key to enable real image creation.

## Requirements

- Node.js 20 or newer
- An OpenAI API key for real image generation (optional; demo mode works without it)

## Run locally

1. Open a terminal in this folder.
2. Run `npm install`.
3. Copy `.env.example` to `.env` and set `OPENAI_API_KEY` to enable real images. Keep the key in `.env`; it is read only by the Express server.
4. Run `npm run dev` and open the Vite URL printed in the terminal (usually `http://localhost:5173`).

For a production preview, run `npm run build`, then `npm start` and open `http://localhost:3001`.

## Workflow

1. Set the topic, category, visual style, color direction, and poster size.
2. Write or edit the three generated prompts in the prompt text boxes, then copy them as needed.
3. Edit an image prompt or upload an image to use as a concept. Generate three images. With a configured key, the server calls the OpenAI Images API; without one, clearly labeled demo illustrations fill the gallery. The backend exposes its configuration state at `/api/status`.
4. Score relevance, composition, clarity, and purpose fit manually from 1–10. Scores are labeled manual and the comparison chart updates as scores change. Select a preferred concept to break a tie.
5. Choose a concept or upload a separate poster background image. Edit poster copy, typography, alignment, color, overlay, dimensions, and optional logo. Export the composed poster as a print-ready PNG (A4 at 2480 × 3508 pixels; other sizes use print-ready dimensions).
6. Print the report or choose “Save as PDF” in the browser print dialog.

Project details are saved in browser local storage and synced to the Express `/api/save` endpoint as local JSON when the backend is running. API secrets must never be placed in frontend source. See `REQUIREMENTS_CHECKLIST.md` for the feature audit and verification results.

## API endpoints

- `GET /api/status` — image API configuration status
- `POST /api/prompts` — create three structured prompt variations
- `POST /api/images` — generate an image using the configured backend API
- `POST /api/evaluate` — request image scores from the configured backend model
- `POST /api/save` — save project JSON to the local `data/` directory

AI-assisted scoring is optional. When an API key is configured, the comparison view offers AI evaluation through the backend; results are labeled AI-assisted and can be adjusted manually.

