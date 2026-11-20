# Edit Review: instructions for an AI assistant

You are reading this because someone wants a video reviewed (or wants to review one) with the Edit Review page.
This file tells you everything needed. You do not have to install or run anything.

## What the page is

One web page (`index.html`, in the same folder as this file). It plays a finished video from a link and lets
the reviewer:

- type notes pinned to the exact moment,
- mark a stretch to cut out (start and end),
- click ready-made notes ("Bad cut", "Zoom here"...),
- draw on the picture to point at something,
- optionally record their voice while they watch.

Nothing is uploaded. When the reviewer saves, the page downloads a `.review.json` file. They send that file to
the person who asked for the review.

## Making a review link

A review session is only an address. Take the page's address (this file's address without `AI.md`; below it is
written `PAGE/`) and add the video:

| The video is | The review link |
|---|---|
| on YouTube (public or unlisted) | `PAGE/?yt=VIDEO_ID` |
| on Google Drive | `PAGE/?drive=FILE_ID` |
| a direct `.mp4` / `.webm` address | `PAGE/?v=URL_ENCODED_ADDRESS` |

- `VIDEO_ID` is the 11 characters of a YouTube link: `youtu.be/VIDEO_ID`, `youtube.com/watch?v=VIDEO_ID`,
  `youtube.com/shorts/VIDEO_ID`, `youtube.com/live/VIDEO_ID`.
- `FILE_ID` is the long part of a Drive link: `drive.google.com/file/d/FILE_ID/view` or `...?id=FILE_ID`.
- The review names itself after the video (its YouTube title, or the file's name), so you don't give a name.
  Only if the person asks for a particular name, add `&s=NAME` (letters, digits, `.`, `_` and `-`).
- If you are unsure, you can also hand over `PAGE/` alone: it has a box where the link is pasted.

Example: the video `https://youtu.be/aqz-KE-bpKQ` becomes `PAGE/?yt=aqz-KE-bpKQ`.

## What to tell the reviewer

1. Open the link in Chrome, Edge or Firefox on a computer (a phone works for typed notes).
2. Play the video. Press **N** to type a note at this moment, **I** and **O** to mark the start and end of a
   stretch to cut, or click a quick-note button. Draw on the picture to point. "Start voice review" is optional.
3. **S** and **E** mark the start and end of a section to write one note about (nothing is cut).
4. Press **Save review** (or finish the voice review). The review is kept on the page under "Your reviews";
   a voice review is written out there so they can check what they said.
5. Press **Download** on the review when they are done. A `.review.json` file lands in Downloads.
6. Send that file back to the person who gave you the link.

## Limits you should know and say

- **Private YouTube videos don't play.** Unlisted and public ones do.
- **Google Drive never plays inside the page** (Drive blocks it). With a Drive link the page asks the reviewer to
  download the video first and then pick the downloaded file; after that everything works the same. For a long
  video a YouTube unlisted link is easier for the reviewer.
- A video file on the reviewer's own computer also works: open `PAGE/` and use "review a video file that is on
  this computer".
- Voice recording needs the page opened from an `https://` address (or `localhost`) and a microphone.
- On YouTube the frame-step keys (`,` and `.`) move by small steps, not exact frames.
- Typed notes that were never saved, and saved reviews not yet downloaded, are still there when the same link is
  opened again in the same browser (not in a private window).
- The first voice review downloads a speech-to-text model (about 80 MB, once). It runs on the reviewer's own
  computer, English only; the review can be downloaded without waiting for it.

## Reading a review file

If someone hands you a `.review.json`, it is JSON with:

- `session`, `name`: the review's name, taken from the video's title. `source`: where the video was. `duration`: its length in seconds.
  `reviewer`: the reviewer's name if they gave one.
- `notes`: the typed notes. Each has `t` (seconds into the video) and `text`. A cut has `cut: true` and `t2`
  (cut from `t` to `t2`; the ends are rough on purpose). A section note has `range: true` and `t2`: the text is
  about everything from `t` to `t2`, and nothing is to be cut. A quick note has `kind` and `group` (`fix` or `idea`).
  `strokes` lists the drawings that belong to the note.
- `strokes`: drawings. Each has `t`, `color` and `pts`, points as fractions of the picture's width and height.
- `audio`: the voice recording, base64 (empty when there is none). `events` is the playhead log recorded with
  it: `w` is seconds into the recording, `t` the video time then, `playing` and `rate` how it was moving. Use it
  to place each spoken sentence on the video.
- `said`: what the page itself made of the recording, for the reviewer to check: lines with `w` (seconds into
  the recording), `t` (video time) and `text`. It can be missing or rough; the recording is the real thing.
- `good`: segments (each `segLen` seconds long, counted from 0) the reviewer marked as good.

## Running the page yourself (only if you can run commands)

It is a static page: any web server works, for example `python -m http.server 8000` in this folder, then
`http://localhost:8000/?yt=VIDEO_ID`. Opening `index.html` straight from disk works for video files on the
computer, but YouTube refuses to play in a page opened that way.
