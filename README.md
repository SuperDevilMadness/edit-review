# Edit Review

A free page for reviewing a video edit: watch it from a link, type notes on exact moments, mark stretches to
cut, draw on the picture, and talk through it if you like. No account and no upload: the review is saved as a
file you send back to the editor.

It is one file, `index.html`, with no server behind it. Live at <https://superdevilmadness.github.io/edit-review/>.

## Review a video

Open the page and paste the video's link, or use a ready-made link:

| The video is | Link | How it plays |
|---|---|---|
| on YouTube (public or unlisted) | `?yt=VIDEO_ID` | In the page. |
| on Google Drive | `?drive=FILE_ID` | Drive doesn't let other pages play its videos, so the page asks you to download the video and pick the file. |
| a direct `.mp4` / `.webm` address | `?v=ENCODED_ADDRESS` | In the page, if the host allows it. |
| a file on your computer | pick it on the page | In the page. |

The review is named after the video: its YouTube title, or the file's name. Adding `&s=NAME` to the link gives it
another name.

Then:

1. Play the video. **N** types a note at this moment, **I** and **O** mark the start and end of a stretch to
   cut, the Fix and Idea buttons add a ready-made note. Draw on the picture to point at something.
2. "Start voice review" records you talking while you watch (optional; needs a microphone).
3. **Save review** downloads a `.review.json` file. Send it to the editor.

Notes you typed but didn't save come back when you open the same link again in the same browser.

## For AI assistants

`AI.md` says how to turn a video link into a review link for someone and how to read a `.review.json`.

## Good to know

- Private YouTube videos don't play; unlisted and public ones do.
- On YouTube the frame-step keys move by small steps, not exact frames, and a paused frame can show YouTube's
  play icon in the middle (YouTube draws it; the page can't remove it).
- A voice review is a big file: about 1.3 MB a minute.
- `quick_notes.json` is the list of Fix and Idea buttons; edit it to change them.
- `&fps=60` in the link sets the size of the frame-step keys (default 30).
- Made for Chrome, Edge and Firefox on a computer. Not tested on phones or in Safari.
