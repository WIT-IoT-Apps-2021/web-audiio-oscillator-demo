# Web Audio Oscillator Demo

[![Node](https://img.shields.io/badge/Node-v14%20LTS-%23339933?style=for-the-badge&logo=node.js)](#requirements)
[![Vue](https://img.shields.io/badge/Vue-3-%234FC08D?style=for-the-badge&logo=vue.js)](https://v3.vuejs.org/)

This is a simple [Vue.js](https://vuejs.org/) web app to demonstrate the basics of oscillators using the Web Audio API [(MDN)](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API).

## Requirements

- Node v14 (Current LTS)

## Running

```bash
npm run dev
```

By default the app should be available on [http://localhost:3000/](http://localhost:3000/).

**Note:** Be sure to access the app via the localhost url and _not_ any of the direct IP addresses. The Web Audio API requires a secure environment (HTTPS) to run but `localhost` is also considered secure while something like `http://127.0.0.1:3000` or `http://192.168.0.10:3000` is not.
