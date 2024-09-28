# VoiceDetectionScripts
Integrate OBS with Streamer Bot to detect sound and pause / resume content

# Step 1: Set Up the Scene and Source

## Create a Scene:

In OBS, navigate to the Scenes section and click the "+" button to create a new scene. You can name it something like "VoiceDetectionScene".

## Add a Source:

In the Sources panel, add a new source (in this case, named "VoiceDetectedSource"). This could be a microphone, audio input, or any other media source you want to monitor for voice detection.
Ensure the source is visible and unlocked (as seen in the second image).

## Source-Specific Filters:

In the VoiceDetectedSource filters panel. Add an effect filter (e.g., "IS_ACTIVE"). It can be anything, it will not be used as an effect, it will only be used to trigger.

# Step 2: Apply Filters to the Source

## Voice Detection Filters:

Open the filters for the Mic/Aux or your audio input by right-clicking on the source in the Sources panel and selecting Filters.

In the Audio Filters tab:

Add an Audio Move filter (called in my example "Voice Detected (Filter Enabler)").
- Meter Type: Set to "Magnitude."
- Easing: Adjust to your preference (90.00 is used in the screenshot).
- Action: Select "Filter Enable."
- Source: Choose your VoiceDetectedSource (the source you added earlier).
- Filter: Select the filter (e.g., "IS_ACTIVE" as in the screenshot).
- Threshold Action: Set to "Enable Over and Disable Under."
- Threshold: Adjust based on how sensitive you want the voice detection to be (0.58 is set in the example).

This filter will enable or disable based on the volume or activity level of the voice input.

Copy this filter and create a second Audio Movefilter to control the visibility of the same source (in my example "Voice Detected (Filter Enabler)").

# Step 3: Set up Streamer Bot

...

# Step 4: Test and Fine-Tune

Once the filters are set up, test the configuration by speaking into your microphone or activating the audio source.
Adjust the Threshold and Easing settings in the filter to ensure the detection is accurate based on your environment.
This setup enables the microphone or audio source to control visibility and transitions based on voice detection, allowing OBS to react dynamically to audio input.
