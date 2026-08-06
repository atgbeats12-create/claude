---
name: atg-mkari-video-playbook
description: "Production playbook for the Atg Mkari talking-head Bible/inspiration/ prophecy/commentary video channel: Google Flow avatar generation, script structure, clip assembly with ffmpeg, thumbnail layout, and multi-platform publishing via Blotato. Use any time Makari asks to write a script, plan a clip list, generate an avatar video, build a thumbnail, assemble clips, or publish a new video for Atg Mkari — even if he just says \"make the next video\" or \"let's do one about [topic]\" without naming tools. Also use for Mkari Studio look/background assets, the stacked/reaction format, end-times prophecy/current-events videos, or Blotato account IDs/captions. Always check this before drafting an Atg Mkari script or touching Flow / Blotato for this channel — it encodes hard-won fixes (content filter workarounds, file size limits, codec-matching) easy to rediscover the hard way."
---

# Atg Mkari Talking-Head Video Playbook

Workflow for producing Bible/inspiration/commentary videos with the Atg Mkari
avatar. Originally written from producing "God Hasn't Forgotten You."

**Core goal:** every video should land on genuine biblical inspiration or
encouragement — a scripture-grounded takeaway the viewer walks away with, not
just a hook for views. Even commentary/news angles should resolve to a
biblical point. If a draft script doesn't have a clear scripture-grounded
takeaway, that's the first thing to fix before touching Flow or Blotato.

## 1. Consistency assets (Google Flow — build once, reuse always)

Project: **"Mkari Studio Commentary"** in Google Flow (labs.google/fx/tools/flow).

- **Character asset**: "Mkari Studio Look (all black)" — built from the
  `@me` avatar. Character Info: "Always wears an all-black outfit — solid
  black button-up shirt buttoned to the top, no other colors or patterns.
  Confident, calm, serious commentator tone for talking-head Bible prophecy
  and news reaction videos."
- **Background asset**: "Mkari Studio Background (modern studio)" — sleek
  modern studio set: clean minimalist backdrop, cool-toned LED/panel
  lighting, subtle geometric or screen-glow accents (no wood paneling or
  bookshelf), generated via Nano Banana 2.
- Tag both with `@` in every generation prompt (video or image) so the look
  and set stay identical across clips and across videos.

If either asset doesn't exist yet in the project, build it first — don't
generate a one-off look for a single video, since that breaks continuity for
every future video.

## 2. Script formats

Ask (or infer from context) which format the video calls for. Default to A
unless Makari signals he wants the reaction/stacked style.

**A. Straight talking-head** (the 4-clip format used for "God Hasn't
Forgotten You"):

Hook → Body (scripture reference) → Application → Close (call to action:
like/subscribe/comment). ~8-10s per clip, 4 clips, ~35-40s total.

Pull the opening line from `ATG_Content_System_Hook_Bank.md`'s ATG Mkari
> section (problem→solution, value promise, authority, contrarian,
> education formulas) and apply the universal rules there: hook lands in the
> first 5 seconds with no wind-up, payoff held for the final 5 seconds, one
> hook tested in 3-5 phrasings rather than shipping the first draft.

This applies to Format B's avatar-hook line too ("you gotta watch this") —
same source, same rules.


**B. Stacked/reaction format** (styled after Traci Coston's channel):

- 3-part vertical stack: top piece / 16:9 source clip in the middle / bottom
  piece. Top and bottom are avatar or graphic elements framing the horizontal
  clip in the center — not a simple 2-way split.
- Sequence: avatar hook ("you gotta watch this") → avatar goes quiet/listening
  while the middle clip plays with captions (loop a short "watching" clip for
  as long as the footage runs) → avatar returns for the closing biblical
  takeaway/encouragement.
- Needs a separate loopable "listening/reacting" avatar clip generated ahead
  of time.
- This same top/middle/bottom arrangement carries over to the thumbnail too
  (see Section 5).

**Content rule (avoid Flow's anti-deepfake filter):** don't have the avatar
make specific factual/political claims about real governments or people —
this gets blocked. Move sensitive facts to on-screen captions instead of
avatar dialogue, or pick a safe angle (inspiration/testimony/scripture) for
anything with a political edge.

**Prophecy / current-events angle:** a recurring content type for this
channel is tying current events — wars and rumors of wars, natural
disasters, technology, geopolitical shifts — to end-times Bible prophecy
(Matthew 24, Daniel, Ezekiel 38, Revelation, etc.). Use Format B for these
so the middle clip can carry the actual news footage. Two things matter
here:

- Keep the avatar's dialogue on the scriptural pattern ("Scripture told us
  to expect this"), not on verifiable claims about a specific named
  government, military, or political figure — same content-filter reason
  as above, and it also keeps the video reading as Bible teaching rather
  than a political take. Put the specific country/event/statistic in the
  on-screen captions over the news footage instead.
- Tone: hope and readiness, not fear or date-setting ("no one knows the day
  or the hour" — Matthew 24:36). The viewer should walk away anchored, not
  anxious — that's the same core goal from the top of this doc, just
  applied to a scarier subject.

## 3. Generating clips

1. In the Flow project, type the script line as quoted spoken dialogue in the
   prompt, tagging both `@Mkari Studio Look` and `@Mkari Studio Background`
   plus a short scene description.
2. Model: Omni Flash, 16:9, 10s clips (~15 credits each).
3. If a generation fails ("Oops, something went wrong"), just retry via the
   Reuse Prompt button — intermittent failures are common and not worth
   troubleshooting further.
4. Clear stray leftover chips/text from the prompt box before building each
   new prompt to avoid contamination from the previous one.

## 4. Downloading & assembling

- Flow's download button produces a `.zip` per clip, not a direct `.mp4` —
  unzip each one.
- Before concatenating, verify codec/resolution/framerate match across clips
  with `ffprobe`. If they match, stream-copy concat is safe and fast:
  ```
  ffmpeg -f concat -safe 0 -i concat_list.txt -c copy output.mp4
  ```
  where `concat_list.txt` lists `file 'clip1.mp4'` etc. in order.
- Flow's auto-titles (e.g. "Man talking about growth") aren't reliable for
  matching a download to its script segment. If unsure which clip is which,
  pull a frame with ffmpeg and eyeball the on-screen text/context.

## 5. Thumbnails

- Generate in Flow's image tool (Nano Banana 2), tagging
  `@Mkari Studio Look` + `@Mkari Studio Background` for any avatar piece.
- **Format: 16:9 horizontal for each piece**, not 9:16 — this keeps the
  pieces stackable while leaving room to crop/edit later.
- **3-part layout** mirroring the video's own arrangement (Section 2B):
  1. Top = hook/topic visual with bold caption-style text (e.g. "YOU NEED TO
     HEAR THIS")
  2. Middle = the actual 16:9 clip
  3. Bottom = avatar host shot with a small channel watermark ("ATG MKARI")
     in a corner

## 6. Publishing (Blotato)

Atg Mkari channel account IDs (from `blotato_list_accounts`):

| Platform | Account ID | Notes |
|---|---|---|
| YouTube | 23788 | requires title, privacyStatus, shouldNotifySubscribers |
| Facebook | 36348 | pageId 1204144956113716 ("Atg Mkari") |
| Instagram | 26926 | username atgmkari; mediaType reel/story |
| Threads | 4263 | username atgmkari |
| TikTok | 25676 | username atg.mkari; requires privacyLevel etc. |
| Twitter | 11249 | username atgmkari |

**Caption pattern** (adapt per video):

- YouTube: "[Title] | Daily Word of Encouragement" — public
- TikTok/IG/FB: 1-2 sentence hook + relevant hashtags (#Faith #BibleVerse
  #Encouragement #Christian)
- Threads/Twitter: scripture references + short teaser line

**Upload constraints:** local files over ~10MB can't go through the standard
browser-upload tool path, and the sandbox network doesn't reach Blotato's
storage domain directly. Workaround: compress first —
```
ffmpeg -vf scale=720:1280 -c:v libx264 -b:v 1400k -c:a aac -b:a 128k
```
— to get under 10MB, then upload via the browser. If this comes up often,
check whether a Blotato web dashboard login offers a smoother path before
defaulting to the compress-and-upload workaround every time.

## 7. Music

If baking in a song from the Awakened Truth Gospel catalog, bake it into the
video file itself before upload — this is the one approach that works on
every platform. Instagram's API supports tagging a named audio track
(`audioName` field) separately if wanted, but TikTok/YouTube/Facebook only
support a generic "auto-add music" toggle, not a specific track — so baked-in
audio is the reliable default across all channels.
