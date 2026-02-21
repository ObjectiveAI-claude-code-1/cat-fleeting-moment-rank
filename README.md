# cat-fleeting-moment-rank

Ranks cat photographs by temporal specificity — the sense that each image could only have been taken at that exact fraction of a second, and that any other fraction would have produced an entirely different photograph.

## Overview

Not every photograph is a moment. Some are merely conditions — a cat sitting, a cat lying still, a cat standing in a neutral pose. These images are indifferent to time. They could have been taken five minutes earlier or five minutes later and looked essentially identical.

`cat-fleeting-moment-rank` finds the other kind: the photographs where time was moving fast and the camera was faster. The cat mid-leap. The slow blink caught at its most closed. The wide-eyed stare of sudden alertness that will soften a heartbeat later. These are images anchored to a precise, unrepeatable instant — moments that were caught, not merely recorded.

The function receives an array of cat photographs and returns a probability distribution ranking them from the most temporally specific to the least.

## Input

The function accepts a single input: an array of cat photographs.

- **Type:** Array of images
- **Minimum items:** 2
- **No metadata required:** No captions, timestamps, breed information, or context of any kind. The image alone must communicate its relationship to time.

```json
{
  "type": "array",
  "minItems": 2,
  "items": {
    "type": "image"
  }
}
```

## Output

The function returns a **vector** — an array of numerical scores, one per input image, that together form a probability distribution summing to approximately 1. Higher scores indicate greater temporal specificity. The scores represent relative rankings: an image's score reflects how temporally specific it is compared to the other images in the same input batch.

## What It Evaluates

The function evaluates three distinct qualities of temporal specificity. Each captures a different dimension of what makes a captured moment feel urgent, lucky, and irretrievable.

### 1. Action Transience

Is the cat's body **between states**? Action transience measures whether the photograph captures a physical configuration that is inherently unstable and passing — a posture the cat cannot hold, only pass through.

**Ranks higher:**
- A body suspended at the apex of a leap
- A mouth open at the peak of a yawn, tongue curled
- A paw striking mid-swing at a toy
- Legs compressing at the instant of landing
- The slow-motion collapse from wakefulness into sleep
- Muscles gathered and coiled just before a spring

**Ranks lower:**
- A cat sitting upright on a surface
- A cat lying flat and relaxed
- A cat standing in a neutral, balanced pose
- Any body at rest in a durable equilibrium

### 2. Expressive Singularity

Does the cat's face reveal a **fleeting micro-expression** specific to that precise instant? Expressive singularity measures whether the configuration of ears, eyes, whiskers, and facial posture captures a transient emotional or sensory signal — something happening inside the cat at that exact moment.

**Ranks higher:**
- Eyes caught at the midpoint of a slow blink
- A squint against a sudden change in light
- Ears rotated backward at a half-heard sound
- Whiskers briefly flattened during a sniff
- The wide, round-eyed stare of sudden alertness
- Ears flattening in response to a startling noise

**Ranks lower:**
- A neutral, relaxed facial expression
- Eyes fully open in a default state
- Ears in a natural forward position
- Any expression indistinguishable from how the cat would look at any other point in time

### 3. Temporal Urgency

Does the entire photograph radiate the sensation of being **lucky**? Temporal urgency is the holistic feeling that a narrow window opened between the cat's unpredictability and the camera's timing, and was seized just before it closed.

**Ranks higher:**
- Scenes where the cat's relationship to its environment is visibly transient (a shaft of light about to shift, a shadow dependent on a posture about to change)
- Images with a sense of narrative imminence — something is about to happen or has just happened
- Photographs where action, expression, and environment all converge in a single unrepeatable instant
- Any image that makes the viewer feel: *this almost didn't get captured*

**Ranks lower:**
- Scenes that would look identical minutes later
- Images where the cat and environment are both in stable, enduring states
- Photographs that sit in the middle of a stillness rather than on the edge of a story
- Any image that could have been taken again with an essentially identical result

## Use Cases

### Content Curation
Surface the most compelling cat photographs from large collections. The images that stop people mid-scroll are rarely the prettiest — they are the ones that feel alive with timing, where the viewer senses they are witnessing something that lasted only an instant.

### Photography Review
Help photographers sift through hundreds of shots from a single session to find the frames where timing elevated the ordinary into something electric — the decisive moments that justify the patience of waiting with a camera.

### Dataset Organization
Organize image datasets along the axis of temporal specificity. Useful for training data selection, quality filtering, or building curated galleries sorted by the urgency of the captured instant.

### Gallery Building
Build collections that prioritize the feeling of *caught moments* over static beauty. Rank and sort personal or editorial photo libraries by how fleeting and unrepeatable each image feels.

## How It Works

The function uses an ensemble of language models to evaluate each photograph across its three quality dimensions. For each dimension, the input images are presented as candidate responses to a prompt that describes the ideal temporally specific photograph. The models score which images most naturally answer the prompt, and the resulting probability distributions are combined into a final ranking.

The three evaluation tasks are:

1. **Action transience prompt** — asks for a cat photograph showing a body in physical transit, frozen in an unstable posture between states
2. **Expressive singularity prompt** — asks for a cat photograph capturing a singular micro-expression that reveals a specific psychological instant
3. **Temporal urgency prompt** — asks for the photograph that feels most like a one-time event, the one that almost didn't get captured

Each task independently ranks all input images. The final output is a weighted combination of all three rankings.

## The Core Question

For every photograph the function evaluates, the fundamental question is the same:

> *If this photograph had been taken one second earlier or later, would it look meaningfully different?*

When the answer is emphatically **yes** — when the moment feels urgent, lucky, and precisely captured — the image ranks high. When the answer is **no** — when the image depicts a state rather than a moment — it ranks low.