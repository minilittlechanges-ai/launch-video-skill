---
name: launch-video
description: "Turn a one-line prompt into a finished, on-brand launch video through a phased agent workflow (brand-frame → storyboard → audio → visuals → render → ship). Use when someone wants to make a launch, promo, or product video from just a brand + topic, instead of hand-editing a timeline. This is a fillable skeleton: fill frame.md with your own brand (colours, type, motion, voice) first, then run the phases in order. The video tool is up to you (Remotion, HyperFrames, etc.); the workflow is the point."
---

# Launch Video Skill

Turn a one-line prompt into a finished, on-brand launch video. The agent does not improvise. It runs the workflow below top to bottom, producing the listed deliverable at each phase before moving on.

This is a **skeleton**. Fill every `⟨…⟩` with your own brand. Once the blanks are filled, you have your own launch-video agent.

## Folder layout

```
launch-video/
├─ SKILL.md          this file · the workflow (the brain)
├─ frame.md          your brand frame (the soul; fill it in)
├─ agents/           frame · story · visual · audio · animate · ship
└─ phases/           the 5 phases below, each hands off a deliverable
```

## Input

```
Make a launch video for ⟨brand⟩, about ⟨topic / angle⟩.
```

One line in, one video out. If it needs ten form fields, it isn't a skill.

## Output

A rendered `.mp4` (default ⟨1080x1350 or 1920x1080⟩), on-brand, with ⟨captions⟩ and ⟨music, no voiceover by default⟩.

## frame.md — your brand (fill this first)

The most important and least copyable part. It holds your taste. The more specific it is, the more the video looks like *you*.

```
Colours   : primary ⟨#HEX⟩, secondary ⟨#HEX⟩, background ⟨#HEX⟩
Type      : display ⟨font⟩, body ⟨font⟩, latin / numbers ⟨font⟩
Motion    : ⟨e.g. staged reveal, no idle wobble, hits on the beat⟩
Voice     : ⟨e.g. casual, conversational, no clickbait⟩
Never use : ⟨your anti-list, e.g. stock icons, white on cream⟩
```

## Agents

One agent, one job. Don't let a single agent do everything.

| Agent | Owns |
|-------|------|
| `frame` | reads frame.md, locks the brand (colour / type / motion) |
| `story` | storyboards: which frame is hook / product / CTA |
| `visual` | per-frame composition, focal point, motion |
| `audio` | music, beat grid, ⟨voiceover on/off⟩ |
| `animate` | renders each frame, assembles the video |
| `ship` | exports, ⟨writes caption / posts to platform⟩ |

## Workflow

1. **brand-frame.** Read `frame.md` first. Lock colours, fonts, motion, voice, and the anti-list before writing a single frame. → Deliverable: locked brand tokens.
2. **storyboard.** Plan the arc: which frame is the hook, which is product, which is CTA; what each frame says and which asset it needs. → Deliverable: a storyboard table (frame · type · line · asset).
3. **audio.** Choose the music and set the beat grid. This format teaches through visuals and rhythm, so captions and cuts land on the beat. → Deliverable: a beat map.
4. **visuals.** Before rendering, direct each frame: composition, focal point, motion. Decide how every element moves and where the eye goes. → Deliverable: per-frame visual direction.
5. **render + ship.** Render each frame, assemble the real video, then Generate, Edit, Ship. → Deliverable: the final `.mp4`, ready to post.

## Rule

Never ask the agent to "just make a great video" in one shot. Run the phases in order and approve each deliverable. **Slow is fast:** lock the brand and storyboard up front, and the render can't go off the rails.

## What this file can't carry

The skeleton is yours. But three things don't travel with it, and these are your real value:

1. **Your brand frame (taste)** — why *this* colour, *this* motion? That's judgment, not config.
2. **Directing each phase** — knowing when the storyboard is wrong, when a render looks like a slideshow, when to re-cut. That's you, not the agent.
3. **The feedback loop** — taking real post-performance data and letting it decide what you make next.

Copy the skeleton. The soul (`frame.md`) and the judgment, you grow yourself.
