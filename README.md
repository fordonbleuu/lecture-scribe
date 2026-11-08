# Lecture Scribe

Live lecture transcription with automatic notes. One HTML file, no build step, no server code, no accounts.

## Run it

The microphone only works from `http://localhost` or an `https` site, so don't just double-click the file.

**On your computer**

```bash
cd lecture-scribe
npm start            # or: node server.js
```

Then open <http://localhost:8000> in Chrome or Edge.

No Node? `python -m http.server 8000` in this folder does the same thing.
The server is only there to serve the file — nothing is uploaded, and no transcript leaves the browser.

**Online**

Drag this folder onto Netlify Drop, or push it to GitHub Pages. You get an `https` link that also works on phones.

## Use it

- Press **Start recording** and allow the microphone.
- Pick the lecture language first. Changing it while recording restarts recognition in the new language.
- Click any transcript line, or press **Mark important**, to force a line into the notes.
- **Import transcript** builds notes from pasted text or a `.txt`, `.vtt` or `.srt` file.
- **Copy notes** or **Download .md** to keep them.
- Hover the top-right icon to switch between light and dark themes.

Keyboard: `Tab` to a transcript line, then `Enter` or `Space` to mark it. `Esc` closes the import panel.

## How the notes are built

Everything runs locally in the browser:

- **Key terms** — words used repeatedly, with their frequency.
- **Sections** — the lecture is split at pauses of ~20s or every ~3 minutes, and titled by its strongest terms.
- **Main points** — sentences scored by keyword density and cue phrases such as "important", "for example", "in summary".
- **Definitions** — sentences that use "is defined as", "means", "refers to".
- **Reminders** — sentences about exams, quizzes, deadlines and submissions.

The notes are a study aid, not a substitute for listening. Review them before relying on them.

## Troubleshooting

**"The microphone is blocked."** Allow the microphone from the icon at the left of the address bar, then press **Try again** on the message. If the page is open as a `file://` URL, use the server instead.

**"Speech recognition could not reach the browser's speech service."** Chrome and Edge send the audio to their vendor's speech service, so this message means that service could not be reached — not that the page is broken. Try, in order:

1. Confirm the machine is actually online.
2. Switch browser. Chrome uses Google's service, Edge uses Microsoft's; if one is blocked, the other usually works.
3. Turn off a VPN, proxy, or antivirus web shield, then reload.
4. In Brave, turn on *Google services for Web Speech API* in `brave://settings/privacy`.
5. School and office networks often block the endpoint. A phone hotspot is a fast way to test.
6. If none of that works, use **Import transcript** with text copied from Zoom, Meet or Teams — that path never needs the microphone.

**Recording runs but no words appear.** Watch the bar next to the timer while you speak:

- **The bar stays empty and says "No input".** The browser is not receiving audio. Pick the right input device and raise its level in your system sound settings, unmute the microphone, and close any app that holds it exclusively (Teams, Zoom, Discord).
- **The bar moves but no text appears.** Audio is fine, so the speech service is not returning words. Try Edge, confirm the selected language matches the speaker, then check the browser console for `[lecture-scribe]` lines, which record the recognition lifecycle.

**The recording button is greyed out.** The browser has no `SpeechRecognition` (Firefox, for example). Use Chrome, Edge or Safari, or import a transcript.

## Notes

- Speech recognition comes from the browser (Chrome, Edge or Safari) and needs an internet connection, because the audio is processed by the browser vendor's service. Nothing is stored on a server by this app.
- Your lecture is saved in this browser only (`localStorage`). Clearing the site data or pressing **Clear** removes it.
- The sample lecture appears on first load so you can see the notes without recording anything.
