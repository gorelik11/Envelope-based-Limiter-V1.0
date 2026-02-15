# Envelope-based Limiter V1.0

A REAPER ReaScript (Lua) that acts as a brick-wall peak limiter by writing precise volume automation envelopes. Instead of using a real-time plugin, it analyzes the audio offline and creates envelope points that tame peaks — giving you full visual control and editability.

## How It Works

1. Reads the selected audio item's waveform using REAPER's AudioAccessor API
2. Scans for peaks exceeding your ceiling threshold
3. Calculates the exact gain reduction needed for each peak (infinity ratio — true brick-wall)
4. Writes volume automation envelope points with configurable attack and release times
5. Merges nearby peaks into smooth regions to avoid rapid automation artifacts

## Parameters

When you run the script, a dialog box appears with four settings:

| Parameter | Default | Description |
|-----------|---------|-------------|
| **Ceiling (dB)** | -9.0 | Maximum allowed peak level. Peaks above this will be reduced. |
| **Attack (ms)** | 10 | How far before the peak the volume starts ducking. |
| **Release (ms)** | 50 | How long after the peak it takes to return to unity gain. |
| **Analysis window (ms)** | 5 | Size of the analysis window. Smaller = more precise but more automation points. |

## Installation

1. Open REAPER
2. Go to **Actions > Show action list**
3. Click **New action > New ReaScript...**
4. Save the file as `Envelope-based Limiter V1.0.lua` (or copy the .lua file to your REAPER Scripts folder)
5. Paste the script contents and save

Alternatively, copy `Envelope-based Limiter V1.0.lua` directly into your REAPER Scripts folder:
- **macOS:** `~/Library/Application Support/REAPER/Scripts/`
- **Windows:** `%APPDATA%\REAPER\Scripts\`
- **Linux:** `~/.config/REAPER/Scripts/`

Then load it via Actions > Show action list > Load ReaScript.

## Usage

1. **Select an audio item** on a track (click on it)
2. Run the script from the Actions list
3. Adjust the parameters in the dialog box (or keep defaults)
4. Click OK — the script will analyze and write automation
5. A summary dialog will show how many peak regions were found

## Important Notes

- **Volume automation is post-FX.** If you need to measure the result with a plugin (like a loudness meter), route the track to a bus and place the meter there.
- **Fully undoable.** Press Ctrl+Z / Cmd+Z to undo the automation if needed.
- The script **clears existing volume automation points** within the selected item's time range before writing new ones.
- Works with stereo and mono audio items.
- Respects take playback rate.

## Requirements

- REAPER v5.0+ (tested on v7.x)
- No additional extensions required — uses only built-in ReaScript API

## License

MIT
