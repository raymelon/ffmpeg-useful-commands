# ffmpeg-useful-commands
useful commands for ffmpeg: trim clips, combine videos, etc.

## make a clip

#### notable flags

| Flag | What | Explain like I'm Five | Example |
| :------ | :---------- | :---------- | --------: |
| `-ss` | start time | _where in the input video the clip starts_ | `-ss 03:13:42` |
| `-t` | time duration | _how long the clip should be_ | `-t 00:10:45` |

#### example
`ffmpeg -ss 03:13:42 -i 'input.mp4' -t 00:10:45 -c copy output.mp4`

