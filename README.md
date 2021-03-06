# canvas-image-scrubber

[![npm version](https://badge.fury.io/js/canvas-image-scrubber.svg)](https://badge.fury.io/js/canvas-image-scrubber)

*Currently under heavy development. API will probably change

A react component to render video-like playback for image sequences 🎥.

[View Demo](https://anni-platform.github.io/canvas-image-scrubber/)

## Installation

Via NPM:

`npm install canvas-image-scrubber`

or Yarn:

`yarn add canvas-image-scrubber`

## Basic Usage with `webpack` and `file-loader`

`frames` is a required prop which must be an array of valid image paths to each frame of your image sequence.

`render` is also a required prop. It is a [render-prop](https://cdb.reacttraining.com/use-a-render-prop-50de598f11ce) which allows you to render the image sequence player, controls, playback progress bar, and audio controls however you wish. See below for basic usage, and `./demo/src/index.js` for more advanced usage with prop getters `getViewerControlsProps` and `getViewerProgressProps`.

More robust documentation will hopefully be coming soon.. 🤠

```js
import React from 'react';
import CanvasImageScrubber from 'canvas-image-scrubber';
export function getFrames() {
  let i = 1;
  const frames = [];
  while (i < 39) {
    frames.push(require(`./frames/Frame-${i}.jpg`));
    i++;
  }
  return frames;
}

const frames = getFrames();

function MyApp() {
  render() {
    <CanvasImageScrubber
      frames={frames}
      render={({ renderViewer }) => {
        return (
          <div>
            {renderViewer}
          </div>
        )
      }}
    />
  }
}
```

## Optionally render your own canvas element

The render props provided in the `render` prop callback provide a `getCanvasRef` which will allow you to render your own canvas element should you need to do so. Use `getCanvasRef` as the value for the prop `ref` on your canvas element, this way `canvas-image-scrubber` can get a dom reference to your canvas element. Usage example:

```js

function MyApp() {
  render() {
    <CanvasImageScrubber
      frames={frames}
      render={({ getCanvasRef }) => {
        return (
          <div>
            <canvas ref={getCanvasRef} />
          </div>
        )
      }}
    />
  }
}

[npm-badge]: https://img.shields.io/npm/v/npm-package.png?style=flat-square
[npm]: https://www.npmjs.com/package/canvas-image-scrubber
