# Speech Recognition UI

Angular 7 + Angular Material front end for turning speech into text. Runs in the browser or as an Electron desktop app.

## Features

- **Speech to text** – live transcription from the microphone using the browser's Web Speech API (via [`@kamiazya/ngx-speech-recognition`](https://github.com/kamiazya/ngx-speech-recognition)). Works in Chromium-based browsers and Electron.
- **Audio file to text** – upload a `.wav` file; it is sent to a backend that returns the transcript.

State of both screens is kept in `AppService`, so switching tabs doesn't lose your text.

## Requirements

- Node.js 10/12 (Angular CLI 7 doesn't run on modern Node; use `nvm use 12` or similar)
- npm or yarn
- A microphone, and a backend for file transcription (see below)

## Getting started

```bash
npm install
npm start            # dev server at http://localhost:4200
```

### Backend

File transcription posts `multipart/form-data` (field `file`) to:

```
POST {apiUrl}/audio-to-text
```

and expects the transcript text in the response. `apiUrl` is set in [`src/environments/environment.ts`](src/environments/environment.ts) (default `http://localhost:80/api/v1`).

> `environment.prod.ts` has no `apiUrl` yet – add it before making a production build, or uploads will fail.

## Scripts

| Command | What it does |
|---|---|
| `npm start` | Dev server with live reload |
| `npm run build` | Build to `dist/speech-recognition-ui/` |
| `npm run electron` | Build and launch in Electron |
| `npm run electron-aot` | Production build and launch in Electron |
| `npm test` | Unit tests (Karma + Jasmine) |
| `npm run e2e` | End-to-end tests (Protractor) |
| `npm run lint` | TSLint |

## Project structure

```
main.js                         Electron entry point (loads dist/ build)
src/app/
  core/                         layout, header, navbar, ApiService (HTTP wrapper)
  modules/
    transform-speech-in-text/   live microphone transcription
    transform-audio-file-to-text/  .wav upload + transcript
    welcome/, special-actions/  placeholders
  shared/
    components/upload-file/     file picker
    services/                   AppService (screen state), UploadFileService
    constants/, models/
```
