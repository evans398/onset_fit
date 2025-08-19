# onset_fit

This repository is for a device that is still under development. The purpose of the device is to pair the Groove Transformer. The Groove Transformer is a transformer-based generative rhythm model that can generate full multi-voice drum patterns. These patterns can be conditioned by a live input such as a MIDI instrument or they can be generated through latent space navigation. 

The Groove Transformer generates 2 bar patterns faster than real-time. Therefore, we know the generated patterns before the onsets are played back. Therefore, the purpose of the onset_fit device is to fit complex modulation curves the generated rhythmic onsets. These modulation curves will align with the generated rhythm and the curves are able to anticipate the onsets because the full 2 bar pattern is already generated.

# Set up

In this prototype device, I am using a modified Groove Transformer plugin that sends out the generated patterns as OSC. These OSC patterns are received by the onset_fit device and stored.
