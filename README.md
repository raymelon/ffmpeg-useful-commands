# ffmpeg-useful-commands
useful commands for ffmpeg: trim clips, combine videos, etc.

## make a clip

**notable flags**

| Flag | What | Explain like I'm Five | Example |
| :------ | :---------- | :---------- | --------: |
| `-ss` | start time | _where in the input video the clip starts_ | `-ss 03:13:42` |
| `-t` | time duration | _how long the clip should be_ | `-t 00:10:45` |

**example**

```bash
ffmpeg -ss 03:13:42 -i 'input.mp4' -t 00:10:45 -c copy output.mp4
```
## combine clips (without re-encoding which is faster and uses less system resources)

**notable flags**

| Flag | What | Explain like I'm Five | Example |
| :------ | :---------- | :---------- | --------: |
| `-i` | input filelist | _a file list txt file containing the paths of the clips to merge_ | `-i filelist.txt` |

**how `filelist.txt` looks like**

```txt
file 'C:\test\clip1.mp4'
file 'C:\test\clip2.mp4'
```

**why no re-encoding?**

Re-encoding is intentionally omitted to save time and system resources.

**when to re-encode?**

FFmpeg allows merging videos with small differences in stream properties, such as framerate (FPS). Overriding minor mismatches (e.g., up to 0.5 FPS difference) enables fast concatenation without re-encoding, which is useful for videos recorded on similar devices or settings. However, merging files with larger differences can cause audio/video sync issues or playback glitches. [Read more on https://github.com/raymelon/ffmpeg-video-quick-merger-gui](https://github.com/raymelon/ffmpeg-video-quick-merger-gui/tree/main?tab=readme-ov-file#why-allow-to-override-minor-stream-mismatches)

Disclaimer: Only override stream mismatches if the FPS difference is 1-3 FPS (e.g., 27.5 vs 30.0). Merging videos with greater differences may result in audio/video de-synchronization or playback problems. Always watch the merged output to ensure there are no sync issues. [Read more on https://github.com/raymelon/ffmpeg-video-quick-merger-gui](https://github.com/raymelon/ffmpeg-video-quick-merger-gui/tree/main?tab=readme-ov-file#why-allow-to-override-minor-stream-mismatches)

**example**

```bash
ffmpeg -f concat -safe -0 -i filelist.txt -c copy output.mp4
```

