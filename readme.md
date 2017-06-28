# audio-buffer-from [![Build Status](https://travis-ci.org/audiojs/audio-buffer-from.svg?branch=master)](https://travis-ci.org/audiojs/audio-buffer-from) [![unstable](https://img.shields.io/badge/stability-unstable-green.svg)](http://github.com/badges/stability-badges)

Create [AudioBuffer](https://github.com/audiojs/audio-buffer) from any source.

## Usage

[![$ npm install audio-buffer-from](http://nodei.co/npm/audio-buffer-from.png?mini=true)](http://npmjs.org/package/audio-buffer-from)

```js
var createBuffer = require('audio-buffer-from')

//mono-buffer 1024 samples
var abuf = createBuffer(1024)

//stereo-buffer 1024 samples
var abuf2 = createBuffer(1024, 2)

//buffer from data with bound audio context
var abuf3 = createBuffer(floatArray, {context: audioContext})

//empty 1-sample mono buffer with default context
var abuf4 = createBuffer()

//0-length no-context buffer
var abuf5 = createBuffer(0)

//from pcm data
var abuf6 = createBuffer(new Uint8Array([0, 0, 255, 255]), 'interleaved 96000')

//from data-uri
var abuf7 = createBuffer('data:application/octet-stream;base64,AP8A/w==', 'uint8')

//from base64 string
var abuf7 = createBuffer('AAAAAAAAAAAAAIA/AACAPw==', 'float32 stereo planar')
```

## API

### audioBuffer = createBuffer(source|length, channels|format|options)

Create audio buffer from any `source` data or a number indicating `length`, pass `options` to ensure output buffer parameters. A `channels` number or `format` string can be used to shorthand options argument.

#### Source

| Type | Interpretation |
|---|---|
| `null` | Blank 1-sample length buffer. |
| `Number` | Length of resulting buffer. |
| `Array` of arrays | Every subarray is considered as channel data. |
| `AudioBuffer` | Clone other AudioBuffer. |
| `Object` | Create based on `length`, `channels` and `sampleRate` properties. |
| `Array` of numbers | Raw data, interpreted by `dtype` and `interleaved` options, defaults to `float32`. |
| `Float32Array` | Raw `float32` data, amplitude range is `-1..+1`. |
| `Float64Array` | Raw `float64` data, amplitude range is `-1..+1`. |
| `Uint8Array` | Raw `uint8` data, amplitude range is `-128..+127`. |
| `TypedArray` | Any other typed array, described by `options.format` argument (see [pcm-convert](https://github.com/audiojs/pcm-convert). |
| `ArrayBuffer` | Raw data, interpreted by `options.format`. |
| `Buffer` | Raw data, interpreted by `options.format`. |
| Base64 string | Data is decoded based on options and handled as `ArrayBuffer`. |
| Data-URI string | Data is decoded based on options and handled as `ArrayBuffer`. |
| `ndarray` | Create from [ndarray](https://npmjs.org/package/ndarray) instance. The `shape` property is considered as `[length, channels]`. |
| `ndsamples` | Create from [ndsamples](https://npmjs.org/package/ndsamples) instance, similar to ndarray. |

#### Options

| Property | Default | Meaning |
|---|---|---|
| `length` | `1` | Resulting buffer length. If `0`, buffer is unbound from context.  |
| `context` | [`audio-context`](https://github.com/audiojs/audio-context) | Audio context to bind. `null`-context creates unbound audio buffer. |
| `channels`, `numberOfChannels` | `1` | Output buffer number of channels. |
| `sampleRate` | `44100` | Output buffer sample rate. |
| `format` | `null` | Source pcm format string or object, see [audio-format](https://github.com/audio-format). If `null`, it will be detected from the `source`. |


### Related

* [audio-buffer](https://github.com/audiojs/audio-buffer)
* [audio-buffer-utils](https://github.com/audiojs/audio-buffer-utils)
* [pcm-convert](https://github.com/audiojs/pcm-convert)
