# vonote

A simple voice note app that runs in your browser. Hit record, talk, hit stop. Your note is saved and you can come back and listen to it whenever.

Live: https://vonote.vercel.app/

I wanted a quick way to say something out loud and hear it later, without making an account or uploading my voice to someone's server. So everything stays on your device.

It started as a speech to text app, but I realised I wanted the actual audio, so I rebuilt it as a voice note app.

## What you can do

- Record, pause, resume and stop
- Notes save automatically when you stop
- Play any note back, drag the waveform to jump around, and change the speed
- Rename, download or delete a note (delete has an undo)
- If your tab crashes or your phone dies mid recording, the app gets back what it recorded next time you open it

Recordings stop at 60 minutes so a forgotten tab doesn't fill up your storage.

## Run it

Just one HTML file, no build step. The mic only works on `localhost` or https, so don't open the file directly.

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000

## Files

- `index.html`: the whole app
- `og.png`: the preview image when you share the link
- `README.md`: this file

## What I used

Plain HTML and JavaScript, Tailwind CSS (CDN), Anime.js for the animations, Lucide for icons, and Inter from Google Fonts. Recording uses the browser's built in MediaRecorder and notes are stored in IndexedDB.

The CDN scripts are pinned to exact versions with integrity hashes. If you change a version, you need to generate a new hash, otherwise the browser will block the script:

```bash
curl -s https://cdn.jsdelivr.net/npm/animejs@4.5.0/dist/bundles/anime.umd.min.js \
  | openssl dgst -sha384 -binary | openssl base64 -A
```

## Things to know

- Your notes live in your browser only. Clear your site data and they're gone, so download the ones you care about.
- Notes don't sync between devices.
- On iPhone, Safari can pause the page when you switch apps or lock the screen, which can cut a recording short. Keep the screen on while recording.
- Downloaded files are `.webm`, `.m4a` or `.ogg` depending on your browser. Some players show the wrong length for the Chrome ones, but they play fine.

## Privacy

Nothing leaves your device. No server, no analytics, no cookies.

## Deploy

It's a static site. On Vercel, import the folder, pick "Other" as the framework, and leave the build command empty.

## Testing

I tested it in headless Chrome with a fake microphone: recording, saving, playback, seeking, renaming, deleting, reloading, and crash recovery. I haven't tried it on a real iPhone yet, so if something breaks on Safari, that's the first place to look.

