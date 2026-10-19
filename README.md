# Lyric Popup Studio

A single-file web page for making vertical (9:16) lyric videos in the style of "coded lyrics" posts. Each lyric line appears in a retro error-dialog popup with an animated emoji, tilted over a filmed-monitor wall of real Java code. You screen-record it and post the clip.

No install or build step is needed. The page and emoji assets are in `lyric_popup.html`. `vercel.json` routes the site root to the page for static hosting.

## Quick start

1. Open `lyric_popup.html` in Chrome, Edge, Firefox or Safari.
2. Select a song with **Song audio**.
3. Import timestamped lyrics (`.lrc`, `.txt`, or `.json`) or paste them into the **Lyrics** box.
4. Press **Play**, or open **Record mode** and start your screen recorder.

The project does not bundle song audio or copyrighted song lyrics. Choose your own local audio and lyrics file.

## Timestamped lyrics and audio

Each line in an `.lrc` file uses an LRC timestamp followed by the lyric text:

```text
[00:10.63]Your lyric line
[00:15.21]Your next lyric line
```

The timestamps are minutes, seconds, and optional hundredths. You can also use `[hh:mm:ss.xx]`. While timestamped lyrics are playing, the popup follows the selected audio's playback position, including when you pause, seek forward or backward, or restart. Timestamp lookup uses a binary search over the sorted timestamps. Empty timestamp-only lines are treated as gaps. Keep every lyric line timestamped for audio sync; untimed lyrics continue to use **Seconds per line**.

You can also paste or load a JSON array of timestamped lines:

```json
[
  { "time": 10.63, "text": "Your lyric line" },
  { "time": 15.21, "text": "Your next lyric line" }
]
```

Use the lyrics file picker to load an `.lrc`, `.txt`, or `.json` file. Choose any browser-supported audio file with **Song audio**. A missing opening `[` before a timestamp is also accepted.

## Controls

| Control | What it does |
| --- | --- |
| Song title | Sets the popup's title and the title string inside the code wall. Updates live. |
| Lyrics box | One line per popup, optionally prefixed with an LRC timestamp. Click any row to preview that line on the stage. |
| Lyrics file | Loads a `.lrc`, `.txt`, or JSON file into the editor. |
| Lyricsify link | Opens Lyricsify in a new tab to find timestamped lyrics. |
| Emoji buttons | Click one to put that emoji on the row you are editing. |
| Play / Pause | Follows timestamps against the song audio, or steps through untimed lyrics automatically. |
| Next | Shows the next line. The popup's OK button and the × do the same. |
| Restart | Goes back to the first line. |
| Seconds per line | How long each untimed line stays up (0.6 to 6 seconds). |
| Song audio | Plays the selected song; timestamped lyrics stay synced to its position. |
| Record mode | Hides the editor and fills the screen with the 9:16 frame. |

### Keyboard shortcuts (outside the text boxes)

- **Space**: play or pause
- **Right arrow**: next line
- **Esc**: leave Record mode

## Choosing emojis

Each line automatically gets an emoji selected from lyric keywords and imagery. Related emojis rotate to avoid repeating the same emoji across nearby lines while preserving the theme. This works for pasted and imported lyrics, including JSON. It runs locally in the page and does not send lyrics to a service. If a line has no recognizable theme, it uses a varied animated emoji fallback. To choose an emoji yourself, start the lyric row with its code and a bar; the manual choice takes precedence over automatic matching:

```
:3: | your lyric line here
!🦋 | another line
```

| Code | Emoji |
| --- | --- |
| `:1:` | Pensive face |
| `:2:` | Squinting face with blush |
| `:3:` | Smiling face |
| `:4:` | Black heart |
| `:5:` | Blushing face with fingers |
| `:6:` | Relieved face with sweat drop |
| `:7:` | Pixel heart |
| `:8:` | Compact disc |
| `:9:` | Pixel flame |
| `:10:` | Sparkle burst |
| `:11:` | Music notes |
| `!🎧` | Black headphones |
| `!🦋` | Black butterfly |
| `!🌹` | Black rose |

A `!` in front of a normal emoji turns it black. You can use any emoji this way, for example `!🥀 | your line`. Without the `!`, a normal emoji keeps its colors and gets a small looping animation (bounce, wiggle, spin, pulse, float or shake).

## Recording a 9:16 video

1. Click **Record mode**. The page goes full screen and shows a 9:16 frame in the middle.
2. Start your screen recorder (OBS, the Windows Game Bar, macOS screen recording, or your phone's recorder if you open the page there).
3. Press **Space** to play. Press **Space** again to pause, or **Esc** to leave.
4. Crop the recording to the centre 9:16 frame in your video editor (CapCut, DaVinci Resolve, and similar) and add your song audio there if you did not use the **Song audio** box.

Tip: to line a line up with the beat, set **Seconds per line** to match the song, or press the right arrow at each beat instead of using Play.

## Customising

Everything is plain HTML, CSS and JavaScript in one file, so you can open it in any text editor.

## Deploying to Vercel

Import this GitHub repository in Vercel and deploy it as a static site with no build command and the repository root as the output directory. The included `vercel.json` serves `lyric_popup.html` at the site's root URL. Song audio is selected by each visitor in their browser and is not uploaded by the site.

- **Colors of the code wall:** the `--k`, `--p`, `--s`, `--n`, `--f` values near the top of the `<style>` block.
- **Dialog size and tilt:** `.dialog` (width) and `.plane` (the `rotateZ`, `rotateY` and `rotateX` values) in the CSS.
- **The code on the wall:** the `SRC` string in the script is ordinary Java source. Replace it with any other code you like. Wrap a parameter name in `⟦ ⟧` to show it as a grey IDE hint, and write `%TITLE%` where you want the song title to appear.
- **Automatic emoji order:** the `pool` list in the script.

## Notes

- Use lyrics you have the right to show. The page ships with editable example lines only.
- The emoji GIFs are shrunk to about 128 pixels to keep the file near 1.2 MB, so they may look slightly softer than the originals.
- If the emojis show as strange characters when you open the file, make sure it is saved as UTF-8 and opened in a modern browser.
- Audio only plays after you press Play, because browsers block sound until you interact with the page.

## Files

- `lyric_popup.html`: the whole project.
- `vercel.json`: static-site root route for Vercel.
- `README.md`: this file.
