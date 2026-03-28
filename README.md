# Party Mode 🎉 (Home Assistant Blueprint)

[![Add this Blueprint to your Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2FSimai00%2Fparty-mode%2Fmain%2Fparty_mode.yaml)

A Home Assistant automation blueprint that turns any button press into a short party scene:

- Plays a sound on selected speakers
- Flashes RGB lights with per-light random colors
- Flashes white/dimmable lights with random brightness
- Restores your previous light + speaker state when done

## What it does

When triggered, the blueprint:

1. Saves the current state of selected lights and media players
2. Sets speaker volume to your configured party level
3. Starts audio playback from a direct file URL
4. Runs randomized light effects for the configured duration
5. Restores the previous scene (applied twice for reliability)

## Requirements

- Home Assistant with Blueprints enabled
- At least one trigger source (button, remote, NFC trigger, etc.)
- Optional but recommended:
  - RGB lights for color effects
  - White/dimmable lights for brightness strobe effects
  - Media players/speakers for party audio

## Installation

### Option A: Manual copy

1. Place [party_mode.yaml](party_mode.yaml) in:
   - `config/blueprints/automation/<your_namespace>/party_mode.yaml`
2. In Home Assistant, go to:
   - **Settings → Automations & Scenes → Blueprints**
3. Create an automation from this blueprint.

### Option B: Import from URL

If this repo is hosted online, use the raw YAML URL in Home Assistant Blueprint import.

## Inputs

- **Party Trigger**: Any trigger (button press, remote action, etc.)
- **Color Lights (RGB)**: Multiple `light` entities
- **White / Dimmable Lights (optional)**: Multiple `light` entities
- **Smart Speakers / Media Players**: Multiple `media_player` entities
- **Party Sound URL**: Direct audio file URL (`.mp3`, `.ogg`, `.flac`, ...)
- **Party Volume**: `0.0` to `1.0`
- **Party Duration**: Approximate effect duration in seconds

## Audio URL notes

Use a **direct file URL**. Streaming page links (YouTube/Spotify/web pages) will not work.

Recommended local hosting:

- Put file in `/config/www/your_sound.mp3`
- Use URL: `http://<HA_HOST>:8123/local/your_sound.mp3`

## Behavior notes

- Automation mode is `single` (new triggers are ignored while running)
- Lights are intentionally desynchronized with random per-light delays
- Scene restore is applied twice with short delays to reduce “stuck on” lights

## Tips

- If your party runs longer than expected with many lights, reduce **Party Duration**
- If you prefer retriggering to restart immediately, change mode from `single` to `restart` in the blueprint
- Start with a moderate volume if multiple speakers are grouped

## Troubleshooting

- **No sound**:
  - Verify media players can play direct URLs
  - Test the URL in a browser on your local network
- **Lights don’t restore perfectly**:
  - Some Zigbee networks/devices can delay commands
  - Keep the built-in restore delays as-is (or increase slightly)
- **Import issues**:
  - Confirm YAML indentation is unchanged
  - Re-copy the file without smart quotes/formatting changes

## License

Use freely in your Home Assistant setup. Add your preferred license here if publishing publicly.
