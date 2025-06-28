[More Plugin](https://vamp-plugins.org/)

---

[Basic pitch linux plugin download](https://github.com/Ircam-Partiels/basic-pitch-vamp-plugin/releases)

---

```python
import tarfile
import os
import shutil

# Extract the tar.gz file
with tarfile.open("Basic-Pitch-Linux.tar.gz", "r:gz") as tar:
    tar.extractall()

# Create the ~/.vamp directory if it doesn't exist
vamp_dir = os.path.expanduser("~/.vamp")
os.makedirs(vamp_dir, exist_ok=True)
os.environ['VAMP_PATH'] = vamp_dir
# Copy the files
shutil.copyfile("Basic-Pitch/ircambasicpitch.so", os.path.join(vamp_dir, "ircambasicpitch.so"))
shutil.copyfile("Basic-Pitch/ircambasicpitch.cat", os.path.join(vamp_dir, "ircambasicpitch.cat"))
```

---

```python
import librosa
import vamp
import pretty_midi
import numpy as np
data,sr = librosa.load('flute.mp3')
output = vamp.collect(data,sr,'ircambasicpitch:basicpitch')
pm = pretty_midi.PrettyMIDI()
instrument = pretty_midi.Instrument(program=0)  # Acoustic Grand Piano

for item in output['list']:
    print(item)
    timestamp = float(item['timestamp'])
    duration = float(item['duration'])
    if 'values' not in item:
        continue
    frequency = item['values'][0]
    velocity_norm = item['values'][1]

    # Convert frequency to MIDI note number
    pitch = int(round(pretty_midi.hz_to_note_number(frequency)))

    # Scale velocity
    midi_velocity = int(round(velocity_norm * 127))
    midi_velocity = max(0, min(127, midi_velocity))  # Clamp

    # Create Note
    note = pretty_midi.Note(
        velocity=midi_velocity,
        pitch=pitch,
        start=timestamp,
        end=timestamp + duration
    )
    instrument.notes.append(note)
pm.instruments.append(instrument)
pm.write('output.mid')
```
