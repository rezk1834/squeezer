# Squeeze

Turns any video into 1, 2, 3, 4 and 5 second time-lapses (60 fps, silent), each containing the whole film. Everything runs in the browser. Nothing is uploaded.

## Deploy to Vercel
Static site, no build step.

- CLI: `cd movie-squeeze && npx vercel --prod`
- or push this folder to GitHub and import it at vercel.com/new (Framework preset: Other, no build command, output directory `.`)

## How it works
- Frames are sampled at evenly spaced times: frame i of an N-frame clip is taken at (i + 0.5) * duration / N. All five clips are collected in a single pass over the movie.
- Decoding: Mediabunny reads the file and uses the browser's WebCodecs `VideoDecoder` (hardware accelerated). If the codec isn't decodable that way, it falls back to a plain `<video>` element seeking frame by frame, which handles whatever the browser can play.
- Encoding: WebCodecs `VideoEncoder` through Mediabunny's MP4 (H.264) and WebM (VP9) muxers.
- Mediabunny is loaded from jsDelivr. To self-host, `npm i mediabunny`, copy its bundle next to index.html, and change the import URL.

## Browser support
Needs WebCodecs encoding: recent Chrome, Edge, Safari. Firefox support varies.
