# svelte-pts-canvas

A Svelte component for the [Pts](https://ptsjs.org) library.

## Installation
```bash
npm install svelte-pts-canvas
```

## Usage
```js
import PtsCanvas from 'svelte-pts-canvas';

// ...

<PtsCanvas setup={{bgcolor: '#f0f'}} onAnimate={handleAnimate} />
```

This is experimental. Take a look at the example in `src/routes/index.svelte`

## Developement

```js
npm run package

cd package
npm publish

```