# Handbells

A browser app that turns songs into falling, color-coded notes for an eight-bell handbell set, so each player watches their own colored lane and rings when a note crosses the line.

**Live site:** https://zealous-island-0bf9f3d10.4.azurestaticapps.net

**With bell sounds:** https://zealous-island-0bf9f3d10.4.azurestaticapps.net/sounds.html

## Features

- **Eight color-coded lanes.** Bells 1–8 map to red, orange, yellow, green, light blue, dark blue, purple, and white (drawn in black so it stays visible). Lanes a song doesn't use are dimmed.
- **Falling notes.** Each note drops down its bell's lane and is "rung" when it crosses the strike line.
- **Tempo control.** A BPM slider (40–200) works while a song is playing, and each song has its own default tempo.
- **Start, pause, and stop.**
- **Optional audio.** `sounds.html` plays a recorded bell sample for each note through the Web Audio API, with a toggle to turn the sound off.

## Songs included

- Jingle Bells (two arrangements)
- Jolly Old St. Nicholas (two arrangements)
- The First Noel
- Joy to the World

## Adding a song

Songs live in `Scripts/songs.js`. Each song is an object with a title, a default tempo, and a list of notes. `note` is the bell number (1–8), and `position` is when it plays, counted in 16th notes from the start:

```js
{
  title: "Jingle Bells",
  defaultBPM: 90,
  notes: [
    { note: 3, position: 0 },
    { note: 3, position: 4 },
    { note: 3, position: 8 },
    // ...
  ]
}
```

At a given BPM, each 16th note lasts `(60 / BPM) / 4` seconds, so changing the tempo rescales the whole song.

## Tech

- Vanilla JavaScript and HTML5 Canvas, animated with `requestAnimationFrame`, with no framework and no build step
- Web Audio API (`AudioContext`, decoded `AudioBuffer`s) for bell playback
- Deployed to **Azure Static Web Apps** through a GitHub Actions workflow on every push to `main`

## Run locally

Serve the folder with any static server so the audio files load, for example:

```bash
npx serve .
```

## License

MIT
