# vdx [![npm Version](https://img.shields.io/npm/v/vdx?cacheSeconds=1800)](https://www.npmjs.org/package/vdx) [![build](https://github.com/yuanqing/vdx/workflows/build/badge.svg)](https://github.com/yuanqing/vdx/actions?query=workflow%3Abuild)

> An intuitive CLI for processing video, powered by [FFmpeg](https://ffmpeg.org)

- Crop, trim, resize, reverse, rotate, strip audio, change the speed, change the frame rate, change the volume, convert to a different file format
- Run multiple operations on multiple files concurrently

## Quick start

*Requires [FFmpeg](https://ffmpeg.org) and [Node.js](https://nodejs.org).*

```sh
$ npm install --global vdx
```

A variety of common video processing operations are supported:

```sh
$ vdx '*.mov' --crop=360,640    # Crop to width 360, height 640
$ vdx '*.mov' --format=gif      # Convert to GIF
$ vdx '*.mov' --fps=12          # Change the frame rate to 12
$ vdx '*.mov' --no-audio        # Strip audio
$ vdx '*.mov' --resize=360,-1   # Resize to width 360, maintaining aspect ratio
$ vdx '*.mov' --reverse         # Reverse
$ vdx '*.mov' --rotate=90       # Rotate 90 degrees clockwise
$ vdx '*.mov' --speed=2         # Double the speed
$ vdx '*.mov' --trim=0:05,0:10  # Trim from time 0:05 to 0:10
$ vdx '*.mov' --volume=0.5      # Halve the volume
```

We can also run multiple operations all at once:

```sh
$ vdx '*.mov' --format=gif --fps=12 --resize=360,640 --speed=2 --trim=0:05,0:10
```

By default, the processed files will be written to a directory called `./build`. To change this, use the `--output` flag:

```sh
$ vdx '*.mov' --format=gif --output='./gifs'
```

By default, up to 3 input files will be processed concurrently. To change this, use the `--parallel` flag:

```sh
$ vdx '*.mov' --format=gif --output='./gifs' --parallel=5
```

## Usage

```
Usage: vdx <pattern> [options]
```

### &lt;pattern&gt;

One or more globs of input files to process.

### [options]

*Use the `-d` or `--debug` flag to print the underlying FFmpeg commands that are being run.*

#### -c, --crop [&lt;x&gt;,&lt;y&gt;,]&lt;width&gt;,&lt;height&gt;

`<x>` and `<y>` both default to `0`.

```sh
# Crop to width 360, height 640
$ vdx '*.mov' --crop=360,640

# Crop to width 360, height 640, starting from coordinates (10, 20)
$ vdx '*.mov' --crop=10,20,360,640
```

#### -f, --format &lt;format&gt;

```sh
# Convert to GIF
$ vdx '*.mov' --format gif
```

#### -fp, --fps &lt;fps&gt;

```sh
# Change the frame rate to 12
$ vdx '*.mov' --fps=12
```

#### -na, --no-audio

```sh
# Strip audio
$ vdx '*.mov' --no-audio
```

#### -o, --output &lt;directory&gt;

`<directory>` defaults to `'./build'`.

```sh
# Output files to './gifs'
$ vdx '*.mov' --format=gif --output='./gifs'
```

#### -p, --parallel &lt;concurrency&gt;

`<concurrency>` defaults to `3`.

```sh
# Process up to 5 files concurrently
$ vdx '*.mov' --format=gif --parallel=5
```

#### -r, --resize &lt;width&gt;,&lt;height&gt;

Set either `<width>` or `<height>` to `-1` to maintain the aspect ratio.

```sh
# Resize to width 360, height 640
$ vdx '*.mov' --resize=360,640

# Resize to width 360, maintaining the aspect ratio
$ vdx '*.mov' --resize=360,-1

# Resize to height 640, maintaining the aspect ratio
$ vdx '*.mov' --resize=-1,640
```

#### -rv, --reverse

```sh
# Reverse
$ vdx '*.mov' --reverse
```

#### -ro, --rotate &lt;angle&gt;

`<angle>` must be one of `-90`, `90`, or `180`.

```sh
# Rotate 90 degrees clockwise
$ vdx '*.mov' --rotate=90

# Rotate 90 degrees counter-clockwise
$ vdx '*.mov' --rotate=-90

# Rotate 180 degrees
$ vdx '*.mov' --rotate=180
```

#### -s, --speed &lt;speed&gt;

```sh
# Halve the speed
$ vdx '*.mov' --speed=0.5

# Double the speed
$ vdx '*.mov' --speed=2
```

#### -t, --trim &lt;start&gt;[,&lt;end&gt;]

Omit `<end>` to trim from `<start>` to the end of the input file.

```sh
# Trim from time 0:05 to the end of the input file
$ vdx '*.mov' --trim=0:05

# Trim from time 0:05 to 0:10
$ vdx '*.mov' --trim=0:05,0:10
```

#### -vo, --volume &lt;volume&gt;

```sh
# Halve the volume
$ vdx '*.mov' --volume=0.5

# Double the volume
$ vdx '*.mov' --volume=2
```

## Installation

```sh
$ npm install --global vdx
```

## Docker

Build:

```sh
$ docker build -t local/vdx .
```

Use:

```sh
$ docker run --rm -u $(id -u):$(id -g) \
    -v /home/me/Videos/:/files/ \
    local/vdx '*.mp4' --output=./output
```

## Prior art

- [fluent-ffmpeg](https://github.com/fluent-ffmpeg/node-fluent-ffmpeg)

## See also

- [FFmpeg Cheatsheet](https://github.com/yuanqing/ffmpeg-cheatsheet)

## License

[MIT](/LICENSE.md)
