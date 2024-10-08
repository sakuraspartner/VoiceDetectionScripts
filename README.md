# VoiceDetectionScripts
Integrate OBS with Streamer Bot to detect sound and pause / resume content

https://github.com/user-attachments/assets/02853a37-7b35-4adf-abc2-0d55b794e6b4

# Step 1: Set Up the Scene and Source

![Scene](OBS-Scene.png)

## Create a Scene:

In OBS, navigate to the Scenes section and click the "+" button to create a new scene. You can name it something like "VoiceDetectionScene".

## Add a Source:

In the Sources panel, add a new source (in this case, named "VoiceDetectedSource"). This could be a microphone, audio input, or any other media source you want to monitor for voice detection.
Ensure the source is visible and unlocked (as seen in the second image).

## Source-Specific Filters:

![audio](OBS-VoiceDetectedSource-filter.png)

In the VoiceDetectedSource filters panel. Add an effect filter (e.g., "IS_ACTIVE"). It can be anything, it will not be used as an effect, it will only be used to trigger.

# Step 2: Apply Filters to the Source

## Voice Detection Filters:

Open the filters for the Mic/Aux or your audio input by right-clicking on the source in the Sources panel and selecting Filters.

In the Audio Filters tab:

Move Transitions are a plugin, that can be downloaded here: https://obsproject.com/forum/resources/move-transition.913/download

Add an Audio Move filter (called in my example "Voice Detected (Filter Enabler)").
- Meter Type: Set to "Magnitude."
- Easing: Adjust to your preference (90.00 is used in the screenshot).
- Action: Select "Filter Enable."
- Source: Choose your VoiceDetectedSource (the source you added earlier).
- Filter: Select the filter (e.g., "IS_ACTIVE" as in the screenshot).
- Threshold Action: Set to "Enable Over and Disable Under."
- Threshold: Adjust based on how sensitive you want the voice detection to be (0.58 is set in the example).

This filter will enable or disable based on the volume or activity level of the voice input.

![filter1](OBS-AudioInput-Filter-1.png)

Copy this filter and create a second Audio Move filter to control the visibility of the same source (in my example "Voice Detected (Filter Enabler)").

![filter2](OBS-AudioInput-Filter-2.png)

# Step 3: Set up Streamer Bot

Import the file `voicedetect.sakurascripts.sb` into your Streamer Bot. A new group will appear called voice with 6 actions. There will also be a new timer.

## Actions

Two actions are important for customization:

- VoiceSource: This will trigger when the enabled state of a source filter is changed (this is the reason for two filters in the audio. It will get the state of the source (you can change the name of the scene and source here if you like) and use the visibility of the source to determine what to do next.
- ToggleDetection: You can define a hotkey (or other trigger) to determine whether the system should be running. When pressed, it will also set the current state of your media playback to ON. This means, you should be watching the content you want to react to, before you press the hotkey. This will allow the detection to work correctly. Otherwise you might end up only playing content when you are talking.

## Timer

The timer can be set in Streamer Bot Settings. It is by default 1 second, but you can increase it if you want more time to speak before it thinks that you are finished. Bear in mind that more time will required more dead air before the content starts up again.

# Step 4: Test and Fine-Tune

Once the filters are set up, test the configuration by speaking into your microphone or activating the audio source.
Adjust the Threshold and Easing settings in the filter to ensure the detection is accurate based on your environment.
This setup enables the microphone or audio source to control visibility and transitions based on voice detection, allowing OBS to react dynamically to audio input.

# Thanks

Thank you to Rondhi from the Streamer.Bot community for their input on creating the connection between Streamer.Bot and OBS to enable voice detection.
