# Edit Review

A free page for reviewing a video edit: watch it from a link, type notes on exact moments, mark stretches to
cut, draw on the picture, and talk through it if you like. No account needed. With a YouTube or Google Drive
link, everyone who has the link sees each other's notes, and **Send** delivers a review to the editor straight away.

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
   cut, **S** and **E** highlight a section to write one note about, the Fix and Idea buttons add a ready-made
   note. Draw on the picture to point at something.
2. "Start voice review" records you talking while you watch (optional; needs a microphone). When you finish,
   the page writes out what you said so you can check it.
3. **Save review** keeps the review on the page, under "Your reviews". Press **Send** there and it reaches the
   editor at once: typed notes, cuts, sections, drawings and what you said, written out. **Download** keeps a
   `.review.json` file copy; it is also how the voice recording itself gets to the editor, since Send carries
   only the written-out words.

## Fixes and sign-off

When the editor has fixed what you noted, the fixes come back on the same link: open it again and look under
**Fixes from the editor**. Each fix shows your note, what was changed and **▶ Watch** (it plays that fix in the
clips video). Mark each one **Looks good** or **Needs more work** (say what), then **Send sign-off**. The editor
gets it straight away.

## Shared notes

With a YouTube or Google Drive link, your notes go online as you write them (put your name in "Your name" so
others know whose they are). Everyone who opens the same link sees them, in teal on the timeline and under
"Notes from others", and adds their own. You can change or remove only your own notes. Notes are stored in a
Google Firebase database run by the editor; anyone who has the link can read that video's notes. Links to a
video file or address don't share: those notes stay on your computer.

Saved reviews stay in your browser, for that video, until you delete them: close the page and they are still
there next time. Notes you typed but didn't save come back the same way.

## For AI assistants

`AI.md` says how to turn a video link into a review link for someone and how to read a `.review.json`.

## Good to know

- Private YouTube videos don't play; unlisted and public ones do.
- On YouTube the frame-step keys move by small steps, not exact frames, and a paused frame can show YouTube's
  play icon in the middle (YouTube draws it; the page can't remove it).
- A voice review is a big file: about 1.3 MB a minute.
- Writing out what you said happens on your own computer (the recording is never uploaded). The first time, the page
  downloads a speech-to-text model (about 80 MB, kept by the browser afterwards) from jsDelivr and Hugging Face.
  It is English only, takes roughly a quarter of the recording's length, and is there for you to check yourself:
  you can download the review without waiting for it, and the editor's side transcribes the recording again.
- A private window keeps saved reviews only while the page is open; the page says so.
- `quick_notes.json` is the list of Fix and Idea buttons; edit it to change them.
- `&fps=60` in the link sets the size of the frame-step keys (default 30).
- Made for Chrome, Edge and Firefox on a computer. Not tested on phones or in Safari.
