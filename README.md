# onset_fit

This repository is for onset_fit, a Max for Live device that is still under development. In its current iteration, onset_fit is meant to be paired with GrooveTransformer. GrooveTransformer is a transformer-based generative rhythm model that generates expressive (micro-timing/velocity) multi-voice MIDI drum patterns that can be conditioned by a live input such as a MIDI instrument or generated through latent space navigation. A NIME paper that discusses an early version hardware Eurorack implementation can be found here: https://repositori-api.upf.edu/api/core/bitstreams/d3c5bfad-7c68-4f6c-b2eb-f046bf69a411/content.

The main purpose of onset_fit is to fit complex, parameterized modulation curves the generated rhythmic onsets (MIDI drum patterns). Since GrooveTransformer generates 2-bar patterns well before playback, onset_fit can look-ahead and fit curves that anticipate onsets rather than only react to them. Much of the design and application of this device was meant to mimic the LFO in Ableton Live. However, rather than using pre-defined shapes or randomness, these modulation curves are closely linked to generated, morphing rhythmic patterns.

## Set up

In this prototype device, I am using a modified Groove Transformer plugin that sends out the generated patterns as OSC. These OSC patterns are received by the onset_fit device and stored. GrooveTransformer plugin is placed on a track in the Ableton Live project and this communication happens in the background, no routing is necessary in Ableton.

## General Overview

The device has three identical vertically-stacked sections. Each of these sections contains its own onset pattern, curve params, modulation destinations, etc. Looking at the device from left to right we have:

1. Preset Bank
2. Playback Direction and Rate Settings
3. Curve Depth and Offset Settings
4. Default and Random Onset Generation (For use without GrooveTransformer)
5. Curve Parameters, Algorithm Selection, Active GrooveTransformer Voices
6. Live Scope / Static View of Onset Pattern
7. Modulation Mapping / Onset MIDI Output

## Preset Bank

Preset Bank saves all parameters for each section

<img width="58" height="176" alt="Screenshot 2025-08-19 at 9 43 00 AM" src="https://github.com/user-attachments/assets/bb7b101f-69a1-4ff8-afba-ad48f9271e05" />

## Playback Direction and Rate Settings

This section defines the rate and direction at which the generated 2-bar loop is played back. The Rate can have three modes: Quantaized Rate by Clock Division (/128 to x64), Rate by Frequency in Hz (0.0 Hz to 40.0 Hz), Manual Scrubbing of the loop with a position parameter (this could be mapped to something like a jog wheel). For Clock Division and Frequency, the direction of playback be set to forward, backward, ping-pong. The Reset button at the top of this section resets the playhead of each loop to position 0. When the Sync Update button is activated, any changes to the Quantized Rate will not take effect until the master clock returns to phase position 0.

<img width="108" height="76" alt="Screenshot 2025-08-19 at 9 53 05 AM" src="https://github.com/user-attachments/assets/8172b232-901a-4f05-aa7a-bf799ff5d15a" />

## Curve Depth and Offset Settings

These controls set the depth of the modulation curve or apply a positive or negative offset to the curve. It should be noted that all modulation curves are shown as bi-polar signals. Therefore, if you apple -100% depth, it will flip the curve vertically around the horizontal axis.

<img width="81" height="57" alt="Screenshot 2025-08-19 at 10 06 22 AM" src="https://github.com/user-attachments/assets/5a9a95f8-82fe-4794-876c-620320df84ea" />

## Default and Random Onset Generation (For use without GrooveTransformer)

These controls allow you to generate a default onset pattern (8 evenly spaced quater-notes) or a randomized onset pattern (every sixteenth-note interval has a 30% chance of an onset)

<img width="44" height="59" alt="Screenshot 2025-08-19 at 10 11 32 AM" src="https://github.com/user-attachments/assets/c3a53aaf-de24-4100-9ce8-d08e8e85348c" />

## Curve Parameters, Algorithm Selection, Active GrooveTransformer Voices

This section is multi-screen and contains the curve parameters. On the first screen, you can select the curve fitting algorithm using the A B C D buttons. Currently only one algorithm has been implemented. The parameters to the right of the algorithm buttons are specific to the chosen algorithm and they are (currently) Sigma, Shape, Skew, Zero. These parameters morph the curve in various way and can be modulated in real-time. The Jitter parameter applies noise the modulation curve. The Rndm button randomized the four algorithm parameters. The Hold button holds the modulation curve at it's current value. Pressing the button in the top right corner takes you to the alternative screen showing the nine generated voices of GrooveTransformer. Here you can selected with voices you want to be active and visible in the 2-bar loop that the modulation curve is fit to.

<img width="165" height="58" alt="Screenshot 2025-08-19 at 10 22 50 AM" src="https://github.com/user-attachments/assets/b1c53f18-4612-4a97-87c0-01cbef790bda" />
<img width="167" height="59" alt="Screenshot 2025-08-19 at 10 23 07 AM" src="https://github.com/user-attachments/assets/8b5b0cff-62ab-4cf8-89ce-889455407771" />


