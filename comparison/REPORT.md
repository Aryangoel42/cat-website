# GTA clipper vs GTA clipper skill — one test run

Source: twitch.tv/kaicenat live (GTA VI), recorded 15:30–15:38 UTC 2026-11-18 (8m20s, 1080p60).
Both tools processed the *same* recording. Private test; do not repost without the streamer's permission.

| | delvo-gta-clipper (live) | gta-clipper-skill (post-hoc) |
|---|---|---|
| Clips from 8m20s | 1 (30s) | 3 (28–30s), my selection from 13 scored windows |
| Selection signal | Chat spike only (131 msgs/10s) | Audio loudness + speech + my transcript read (no chat: none for local file) |
| Clip content | Driving with radio music; captions were song lyrics. Spike with no real moment | Baby reveal, chat-decided stash money, opinion on GTA style |
| Hook title | none | yes (emoji glyph rendered as a box in clip 1) |
| Captions | spoken, whole-line | word-by-word highlight |
| Output | 1080x1920 | 1080x1920 |
| Time cost | real-time (recording); clip render in seconds | transcribe ~1 min, render 3m15s for 3 clips (CPU) |
| Needs | live stream + chat | any video file/link |

## Findings
- Clipper chat reading needs raw TCP to irc.chat.twitch.tv:6697, blocked in this sandbox. Tested via a WebSocket copy (clipper_ws.py); original untouched. Not an issue on a normal machine.
- Clipper process exited at ~15:38 (about 8 min in, cap was 25); cause not confirmed.
- Skill bug: requirements.txt does not pin `av`; transcription crashed (`metadata_errors`). Fix: `av>=11,<17`, as in the clipper's requirements.
- Chat spikes alone fired on a quiet in-game moment; the skill's picks are more content-aware but need Claude's judgment and a full recording.
- Caveat: n=1 stream, 8 minutes, 1 clipper clip. Not statistically meaningful; the skill's picks were chosen by me, not purely automatic.

Files: comparison/clipper/, comparison/skill/ (video and preview files are kept local, not committed: third-party stream footage).
