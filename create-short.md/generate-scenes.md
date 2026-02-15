---
description: Generate scene-by-scene AI video prompts from a completed script for Higgsfield Cinema Studio
arguments:
  - name: script
    description: Path to the script file (.md). Required.
    required: true
  - name: formula
    description: Path to formula file for visual defaults (e.g., knowledge/formulas/@julianealborna-short-form.md). Optional.
    required: false
---

# /generate-scenes - AI Visual Scene Generation

Takes a completed short-form script and generates scene-by-scene production prompts for Higgsfield Cinema Studio AI video generation. Makes intelligent camera, lens, and aperture decisions based on scene type, emotional tone, and narrative purpose.

---

## AVAILABLE EQUIPMENT (Higgsfield Cinema Studio)

### Cameras

| Camera | Best For | Character |
|--------|----------|-----------|
| Full frame Cine Digital | Talking-head, dialogue scenes | Clean, modern, cinematic. Default look. |
| Premium Large Format Digital | Hero shots, emotional climaxes | Extra shallow DOF, premium feel |
| Modular 8K Digital | Wide establishing shots, detail shots | Maximum resolution, versatile |
| Grand Format 70mm Film | Epic/philosophical moments | Film grain, grandeur, weight |
| Studio Digital S35 | Standard coverage, b-roll | Workhorse, neutral |
| Classic 16mm Film | Flashbacks, raw/intimate moments | Grain, texture, nostalgia |

### Lenses

| Lens | Best For | Character |
|------|----------|-----------|
| Warm Cinema Prime | Talking-head default | Warm rendering, natural skin tones, subtle glow |
| Premium Modern Prime | Clean b-roll, research visuals | Sharp, clinical precision |
| Classic Anamorphic | Cinematic dialogue, widescreen feel | Horizontal flares, oval bokeh |
| Compact Anamorphic | Tighter anamorphic for close-ups | Anamorphic character in close range |
| 70s Cinema Prime | Vintage/retro scenes, nostalgic moments | Period-appropriate softness |
| Soviet Vintage Prime | Gritty, raw moments | Imperfect, character-rich rendering |
| Creative Tilt Lens | Miniature/surreal effect | Selective focus plane |
| Extreme Macro | Detail shots (objects, textures) | Ultra-close, abstract |
| Swirl Bokeh Portrait | Dreamy portrait moments | Distinctive swirling background blur |
| Halation Diffusion | Emotional peaks, romantic scenes | Light bleed, ethereal glow |
| Clinical Sharp Prime | Scientific/data visuals, clean graphics | Maximum sharpness, zero personality |

### Focal Lengths

| Focal | Use Case | Effect |
|-------|----------|--------|
| 8mm | Ultra-wide establishing, surreal/distorted POV | Extreme perspective distortion, immersive |
| 14mm | Wide environmental, showing context | Wide but less distorted |
| 35mm | Standard dialogue, medium shots | Natural perspective, versatile |
| 50mm | Close-ups, talking-head, portraits | Human-eye perspective, intimate |

### Aperture

| Aperture | Use Case | Effect |
|----------|----------|--------|
| f/1.4 | Talking-head, portraits, emotional moments | Maximum background blur, subject isolation |
| f/4 | Standard scenes, mild separation | Balanced DOF, some background visible |
| f/11 | Wide shots, environments, everything sharp | Deep focus, darker |

### Genre Tags

Available genres that affect overall mood and color treatment:
- **Intimate** - Warm, close, personal
- **Suspense** - Tension, shadows, uneasy
- **Spectacle** - Grand, epic, awe
- **Western** - Period, dusty, classical
- **Auto** - Let the system decide based on content

---

## DEFAULT CAMERA RIGS (Per Scene Type)

These are the recommended defaults. They can be overridden per scene.

### Talking-Head (Speaker to camera / character reacting)

```
Camera: Full frame Cine Digital
Lens: Warm Cinema Prime
Focal: 50mm
Aperture: f/1.4
Movement: Static or very slow zoom-in for emphasis
Genre: Intimate
```

### Dialogue Scenes (Two characters together)

```
Camera: Full frame Cine Digital
Lens: Classic Anamorphic or Warm Cinema Prime
Focal: 35mm
Aperture: f/1.4
Movement: Static, occasional slow pan between characters
Genre: Intimate or Suspense (depending on tension)
```

### Research / Data Visualization

```
Camera: Studio Digital S35
Lens: Clinical Sharp Prime or Premium Modern Prime
Focal: 35mm
Aperture: f/4
Movement: Slow zoom in on key data
Genre: Auto
```

### Emotional Climax / Revelation Moment

```
Camera: Premium Large Format Digital
Lens: Halation Diffusion or Warm Cinema Prime
Focal: 50mm
Aperture: f/1.4
Movement: Slow push-in
Genre: Intimate or Spectacle
```

### Flashback / Historical Reference

```
Camera: Classic 16mm Film or Grand Format 70mm Film
Lens: 70s Cinema Prime or Soviet Vintage Prime
Focal: 35mm
Aperture: f/4
Movement: Handheld drift or static
Genre: Suspense or Western (period-appropriate)
```

### Environmental / Establishing Shots

```
Camera: Modular 8K Digital
Lens: Premium Modern Prime
Focal: 14mm or 8mm
Aperture: f/11
Movement: Slow pan or truck
Genre: Spectacle
```

### Detail Shots / Metaphor Close-Ups

```
Camera: Full frame Cine Digital
Lens: Extreme Macro or Premium Modern Prime
Focal: 50mm
Aperture: f/1.4
Movement: Static or slow rack focus
Genre: Intimate
```

---

## PHASE 0: INPUT

### 0.1 Load Script

Read the script file at `$ARGUMENTS.script`.

### 0.2 Load Formula Visual Guide (if provided)

If `$ARGUMENTS.formula` is provided, read the formula file and extract:
- Visual Production Guide section
- Default camera setups per scene type
- Color grading preferences
- Cut frequency targets
- B-roll strategy

If no formula provided, use the default camera rigs from this document.

### 0.3 Present Overview

```
"**Script loaded:** {title}

Duration: ~{X} seconds
Sections identified: {count}
Format: {monologue / dialogue / mixed}

Ready to break down into scenes."
```

---

## PHASE 1: SCENE BREAKDOWN

### 1.1 Parse Script into Scenes

Read through the script and identify individual scenes. A new scene starts when:
- The visual setting changes
- A new speaker starts (in dialogue)
- The visual mode shifts (talking-head -> b-roll -> animation)
- A text overlay appears or disappears
- The emotional tone shifts significantly

### 1.2 Classify Each Scene

For each scene, determine:

**Scene Type:**
- Talking-head (one person speaking to camera)
- Dialogue (two people in conversation)
- B-roll (supporting visual, no speaker visible)
- Animation/graphic (scientific diagram, text on black, etc.)
- Detail shot (close-up of object, metaphor visualization)
- Establishing (wide shot of environment)
- Transition (visual bridge between sections)

**Emotional Tone:**
- Curious (opening questions, exploration)
- Tense (conflict, disagreement, data shock)
- Shocked (revelation moment, "lo loco de esto es que...")
- Reflective (processing, silence, acceptance)
- Empowered (resolution, agency, "la buena noticia es...")
- Playful (humor, physical comedy, light moments)
- Serious (data, research, gravity)

**Narrative Function:**
- Hook (attention grab, first impression)
- Setup (context, scene establishment)
- Escalation (building tension, rising stakes)
- Data shock (surprising number or finding)
- Revelation (the "aha" moment, metaphor)
- Resolution (empowerment, philosophical close)
- Punchline (physical action, humor, callback)

**Characters Present:**
- Speaker A (describe appearance, emotion, action)
- Speaker B (describe appearance, emotion, action)
- Neither (b-roll, animation, etc.)

**Duration Estimate:**
- In seconds, based on script text length and pacing notes

### 1.3 Present Scene Breakdown

```
"**Scene Breakdown**

| # | Time | Type | Emotion | Function | Duration | Characters |
|---|------|------|---------|----------|----------|------------|
| 1 | 0:00 | {type} | {emotion} | {function} | {Xs} | {who} |
| 2 | 0:0X | {type} | {emotion} | {function} | {Xs} | {who} |
...

Total scenes: {N}
Estimated duration: {X} seconds

Does this breakdown look right? Want to split or merge any scenes?"
```

---

## PHASE 2: CAMERA RIG SELECTION (Per Scene)

### 2.1 Auto-Select Camera Rigs

For each scene, based on scene type + emotional tone + narrative function, select:

1. **Camera sensor** (which camera body)
2. **Lens** (which lens character)
3. **Focal length** (field of view)
4. **Aperture** (depth of field)
5. **Camera movement** (static, zoom, pan, push-in, handheld)
6. **Speed ramp** (linear, slow-mo, speed-up)
7. **Genre tag** (mood/color treatment)

**Decision Logic:**

```
IF scene_type == "talking-head":
  -> Full frame Cine Digital + Warm Cinema Prime + 50mm + f/1.4
  IF emotion == "empowered" or function == "revelation":
    -> Consider: Premium Large Format + Halation Diffusion (upgrade for impact)
  IF emotion == "serious" and function == "data_shock":
    -> Consider: Studio Digital S35 + Clinical Sharp Prime (clinical feel)

IF scene_type == "dialogue":
  -> Full frame Cine Digital + Classic Anamorphic + 35mm + f/1.4
  IF emotion == "tense":
    -> Genre: Suspense
  IF emotion == "playful":
    -> Genre: Intimate

IF scene_type == "b-roll" or "animation":
  -> Studio Digital S35 + Premium Modern Prime + 35mm + f/4
  IF function == "revelation" (metaphor visualization):
    -> Premium Large Format + Warm Cinema Prime + 50mm + f/1.4

IF scene_type == "detail":
  -> Full frame Cine Digital + Extreme Macro + 50mm + f/1.4

IF scene_type == "establishing":
  -> Modular 8K Digital + Premium Modern Prime + 14mm + f/11

IF function == "hook" and scene_type == "dialogue":
  -> Movement: Static (don't distract from the dialogue)

IF function == "revelation":
  -> Movement: Slow push-in (draw the viewer closer)

IF function == "resolution":
  -> Movement: Static or very subtle (let the message land)

IF emotion == "shocked":
  -> Speed ramp: Brief slow-mo on the reaction
```

### 2.2 Present Full Storyboard

```
"**Camera Rig Selections**

**Scene 1: {brief description}** ({Xs})
- Camera: {sensor}
- Lens: {lens}
- Focal: {focal}mm @ {aperture}
- Movement: {movement}
- Speed: {linear / slow-mo / speed-up}
- Genre: {genre}

**Scene 2: {brief description}** ({Xs})
...

Any overrides? You can change any selection for any scene."
```

```
AskUserQuestion:
Question: "Camera rig selections look good?"
Header: "Rigs"
Options:
  - label: "Looks good (Recommended)"
    description: "Proceed to prompt generation"
  - label: "I want to override some"
    description: "I'll specify which scenes to change"
multiSelect: false
```

If override: accept per-scene changes, update selections.

---

## PHASE 3: PROMPT GENERATION (Per Scene)

### 3.1 Generate Higgsfield Prompts

For each scene, generate a complete Higgsfield Cinema Studio prompt:

**Prompt Structure:**

```
[SCENE DESCRIPTION]
A detailed, visual description of what's happening in the scene.
Include: setting, lighting, composition, subject position, background elements.
Be specific about colors, textures, atmosphere.

[CHARACTER DIRECTION] (if applicable)
Describe character appearance, clothing, expression, emotion, action.
Be specific about age, ethnicity, styling, body language.

[CAMERA NOTES]
Camera: {sensor} + {lens} + {focal}mm @ {aperture}
Movement: {movement description}
Speed: {speed ramp}
Genre: {genre}
```

**Example prompt for talking-head scene:**

```
A young Latino man in his late 20s sits in a warmly lit room, speaking directly
to camera with genuine curiosity in his eyes. The background is softly blurred,
showing hints of a modern living room with warm amber lighting. His expression
shifts from playful questioning to focused intensity. Natural window light
creates soft highlights on his face. He wears a simple dark t-shirt.

Camera: Full frame Cine Digital + Warm Cinema Prime + 50mm @ f/1.4
Movement: Static, very subtle zoom-in over the duration
Genre: Intimate
```

**Example prompt for b-roll/animation scene:**

```
A stylized 2D animation on a deep black background. A green field of grass
fills the lower third of the frame. A single luminous white line traces a path
across the grass, creating a faint trail. The line repeats, and with each pass
the trail deepens, turning from faint impression to worn dirt path to paved road
to a glowing highway. Warm gold particles float upward from the highway.

Camera: Studio Digital S35 + Clinical Sharp Prime + 35mm @ f/4
Movement: Slow zoom into the highway as it forms
Genre: Auto
```

### 3.2 Present All Prompts

```
"**Scene Prompts**

---

**Scene 1** | {time} | {type} | {duration}s
Script: "{The line(s) being spoken}"

**Prompt:**
{Full Higgsfield prompt}

**Camera:** {sensor} + {lens} + {focal}mm @ {aperture}
**Movement:** {movement}
**Genre:** {genre}

---

**Scene 2** | {time} | {type} | {duration}s
...

Review the prompts. Any to refine?"
```

```
AskUserQuestion:
Question: "Prompts ready for production?"
Header: "Prompts"
Options:
  - label: "All good (Recommended)"
    description: "Proceed to sequence planning"
  - label: "Refine some"
    description: "I want to adjust specific prompts"
multiSelect: false
```

---

## PHASE 4: SEQUENCE PLANNING

### 4.1 Group Scenes into Sequences

Higgsfield Cinema Studio works with multi-shot sequences. Plan groupings:

**Rules:**
- Maximum 6 shots per sequence
- Maximum 12 seconds per sequence
- Group by visual continuity (same setting, same characters)
- Plan transitions between sequences

### 4.2 Plan Shot Durations

For each scene within a sequence:
- Talking-head: 2-5 seconds
- B-roll: 1-4 seconds
- Detail: 1-3 seconds
- Dialogue: 2-5 seconds per speaker
- Animation: 3-8 seconds

### 4.3 Plan Transitions

Between sequences:
- Hard cut (default, most common)
- Match cut (same composition, different content)
- Zoom transition (zoom into detail, zoom out to new scene)

### 4.4 Present Sequence Plan

```
"**Sequence Plan**

**Sequence 1** ({X}s total, {N} shots)
| Shot | Scene # | Duration | Type | Transition Out |
|------|---------|----------|------|---------------|
| 1 | {N} | {X}s | {type} | Hard cut |
| 2 | {N} | {X}s | {type} | Hard cut |
...

**Sequence 2** ({X}s total, {N} shots)
...

Total sequences: {N}
Total duration: {X}s

Does the sequence flow work?"
```

---

## PHASE 5: OUTPUT

### 5.1 Save Production Files

Determine save path:
- If invoked from `/create-short`: use the same directory as the script
- If standalone: ask for output path or use `drafts/shorts/standalone/`

**Scenes file:** `{path}/{date}_{slug}-scenes.md`

```yaml
---
title: "{Title}"
script_source: "{path to script}"
formula: "{formula if used}"
total_scenes: {N}
total_sequences: {N}
estimated_duration: "{X}s"
created_at: "{date}"
---

# Scene Production Sheet: {Title}

## Summary
- **Total scenes:** {N}
- **Total sequences:** {N}
- **Estimated duration:** {X} seconds
- **Equipment used:** {unique cameras, lenses listed}

---

## Scenes

### Scene {N} | {timestamp} | {duration}s

**Script:** "{The line(s) spoken in this moment}"

**Higgsfield Prompt:**
{Full prompt text, ready to paste}

**Camera:** {sensor} + {lens} + {focal}mm @ {aperture}
**Movement:** {movement type} + {speed ramp}
**Genre:** {genre}
**Characters:** {character descriptions + emotions}
**Duration:** {X seconds}
**Notes:** {special instructions}

---

{Repeat for all scenes}
```

**Storyboard file:** `{path}/{date}_{slug}-storyboard.md`

```yaml
---
title: "{Title}"
total_sequences: {N}
created_at: "{date}"
---

# Storyboard: {Title}

## Sequence Plan

### Sequence 1 ({X}s, {N} shots)

| Shot | Scene | Duration | Camera | Lens | Focal | Aperture | Movement | Genre | Transition |
|------|-------|----------|--------|------|-------|----------|----------|-------|------------|
| 1 | {N} | {X}s | {cam} | {lens} | {mm} | {f/X} | {move} | {genre} | {transition} |
...

### Sequence 2 ({X}s, {N} shots)
...

## Production Notes

### Color Grading
{Overall color direction based on formula/mood}

### Audio Sync Points
{Key moments where visual must sync with audio: data shocks, pauses, reveals}

### Key Transitions
{Notable transitions and their purpose}
```

### 5.2 Confirm Save

```
"**Production files saved!**

- {path}/{date}_{slug}-scenes.md ({N} scenes with Higgsfield prompts)
- {path}/{date}_{slug}-storyboard.md ({N} sequences planned)

Each scene prompt is ready to paste into Higgsfield Cinema Studio.

Production status: Ready for AI video generation"
```

---

## CINEMATOGRAPHY DECISION PRINCIPLES

These guide the automated camera rig selection:

1. **Emotional moments get shallow depth.** When the viewer should FEEL, isolate the subject (f/1.4, warm lens, close focal).

2. **Data moments get clinical depth.** When the viewer should THINK, show information clearly (f/4, sharp lens, wider focal).

3. **Revelations get upgraded equipment.** The "aha" moment deserves the premium camera and lens. This is the visual climax.

4. **Hooks stay simple.** Don't compete with the dialogue for attention. Static camera, standard rig, let the words hook.

5. **Resolution slows down.** Both visually and in movement. The camera settles as the message lands.

6. **Historical/flashback gets film texture.** 16mm grain or 70mm weight signals "this happened in the past."

7. **Metaphor visualizations get macro or wide.** Depending on whether the metaphor is intimate (macro) or grand (wide).

8. **Comedy gets the most normal rig.** Physical comedy works best when the camera is neutral. The humor comes from the action, not the cinematography.

9. **Consistency within sequences.** Don't switch camera bodies within a 12-second sequence unless there's a strong narrative reason.

10. **The viewer shouldn't notice the camera.** If a rig choice draws attention to itself, simplify. The story comes first.

---

## ERROR HANDLING

| Error | Action |
|-------|--------|
| Script file not found | Ask for correct path |
| Script has no visual direction notes | Infer from script text and formula |
| Formula file not found | Use default camera rigs from this document |
| Too many scenes for Higgsfield sequences | Split into more sequences, max 6 shots each |
| Character description unclear | Ask user for physical description |
| Scene type ambiguous | Ask user to clarify what should be shown |

---

## NOTES

1. **Prompts are ready to paste** - Each scene prompt can go directly into Higgsfield Cinema Studio
2. **Camera rigs are recommendations** - The user can override any selection
3. **Cinematography serves story** - Every equipment choice has a narrative reason
4. **Consistency matters** - Maintain visual language within sequences
5. **Audio sync is critical** - Note where visual must match spoken word precisely

---

*Part of Creator OS Content System*
*Version: 1.0 - AI Visual Scene Generation for Higgsfield Cinema Studio*
*Created: February 2026*
