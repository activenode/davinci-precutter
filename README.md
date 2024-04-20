# Davinci Precutter

## The problem

Given multiple sources (screen recording and cam recording) with both having audio (important!) the audio will often be out of sync.
Syncing videos per audio or syncing 2 videos at all **isn't the big problem to solve here** but it's part of the solution.

The problem however is cutting those sources in a way that will remove the silent parts as this is cumbersome, time-consuming work.

## The idea

1. Sync the sources by detecting the syncing point (can be done pretty will by running `syncstart -s videoA.mkv videoB.mkv` which will return the offset. It will return something like `{'videoB.mkv', 1.942120}`
1. Cut the offset via `ffmpeg -ss 1.942120 -i videoB.mkv -vcodec copy -acodec copy fixed_videoB.mkv`
1. Use `auto-editor fileName.mkv --margin 0.2sec --export premiere` to create an XML file with the cuts to be imported in DaVinci. Then, if feasible, use the exact same file and replace the filename and clip name occurences to meet with the other file
1. Now both files should be well-cut in davinci/premiere whatever and can still be changed. They should align
1. If they don't, we can also sync them from the end and make a cut off at the end. This will ensure they can be in exact sync



## Tools

### `syncstart`

https://github.com/rpuntaie/syncstart

### `auto-editor`

https://github.com/WyattBlue/auto-editor/
