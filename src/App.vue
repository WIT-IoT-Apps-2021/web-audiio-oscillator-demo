<template>
  <div class="container">
    <div class="row">
      <div class="col-6 mt-2">
        <div v-if="!playing">
          <button class="btn btn-success" @click="playPause"><span class="iconify" data-icon="mdi:play" data-inline="true"></span> Play</button>
        </div>
        <div v-else>
          <div class="btn-group" role="group">
            <button class="btn btn-danger" @click="playPause"><span class="iconify" data-icon="mdi:stop" data-inline="true"></span> Stop</button>
            <button class="btn btn-warning" @click="debug = !debug"><span class="iconify" data-icon="mdi:code-json" data-inline="true"></span>Toggle Debug Info</button>
          </div>
        </div>
        <div class="row" v-if="playing">
          <div class="col-sm-4">
            <h3>Frequency Options</h3>
            <label for="freq1" class="form-label">Frequency 1: {{ freq1 }} Hz ({{ wave1 }})</label>
            <input type="range" min="0" max="1200" step="1" class="form-range" id="freq1" v-model="freq1" @change="updateFreq1()" />
            <label for="freq2" class="form-label">Frequency 2: {{ freq2 }} Hz ({{ wave2 }})</label>
            <input type="range" min="0" max="1200" step="1" class="form-range" id="freq1" v-model="freq2" @change="updateFreq2()" />
            <label for="freq3" class="form-label">Frequency 3: {{ freq2 }} Hz ({{ wave3 }})</label>
            <input type="range" min="0" max="1200" step="1" class="form-range" id="freq1" v-model="freq3" @change="updateFreq3()" />
            <button class="btn btn-warning" @click="randomFreq()"><span class="iconify" data-icon="mdi:dice-multiple" data-inline="true"></span> Randomise Frequency</button>
          </div>
          <div class="col-sm-4">
            <h3>Wave Type</h3>
            <div class="btn-group mt-4" role="group">
              <button type="button" class="btn btn-primary" @click="updateWave(1, 'sine')"><span class="iconify" data-icon="mdi:sine-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(1, 'square')"><span class="iconify" data-icon="mdi:square-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(1, 'triangle')"><span class="iconify" data-icon="mdi:triangle-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(1, 'sawtooth')"><span class="iconify" data-icon="mdi:sawtooth-wave" data-inline="true"></span></button>
            </div>
            <br />
            <div class="btn-group mt-4" role="group">
              <button type="button" class="btn btn-primary" @click="updateWave(2, 'sine')"><span class="iconify" data-icon="mdi:sine-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(2, 'square')"><span class="iconify" data-icon="mdi:square-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(2, 'triangle')"><span class="iconify" data-icon="mdi:triangle-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(2, 'sawtooth')"><span class="iconify" data-icon="mdi:sawtooth-wave" data-inline="true"></span></button>
            </div>
            <br />
            <div class="btn-group mt-4" role="group">
              <button type="button" class="btn btn-primary" @click="updateWave(3, 'sine')"><span class="iconify" data-icon="mdi:sine-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(3, 'square')"><span class="iconify" data-icon="mdi:square-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(3, 'triangle')"><span class="iconify" data-icon="mdi:triangle-wave" data-inline="true"></span></button>
              <button type="button" class="btn btn-primary" @click="updateWave(3, 'sawtooth')"><span class="iconify" data-icon="mdi:sawtooth-wave" data-inline="true"></span></button>
            </div>
          </div>
        </div>
        <div class="row" v-if="playing">
          <div class="col-sm-6">
            <h3>Chords</h3>
            <div class="btn-group mt-4" role="group">
              <button type="button" class="btn btn-primary" @click="setChord('CMajor')">C Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('DMajor')">D Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('EMajor')">E Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('FMajor')">F Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('GMajor')">G Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('AMajor')">A Major</button>
              <button type="button" class="btn btn-primary" @click="setChord('BMajor')">B Major</button>
            </div>
          </div>
        </div>
      </div>
      <div class="col-6" v-if="debug">
        <h3>Debug</h3>
        <h4>General</h4>
        <ul>
          <li>Playing: {{ playing }}</li>
          <li>aCtx: {{ aCtx }}</li>
          <li>mainGain: {{ mainGain }}</li>
        </ul>
        <h4>Osc1</h4>
        <ul>
          <li>osc1: {{ osc1 }}</li>
          <li>freq1: {{ freq1 }}</li>
          <li>wave1: {{ wave1 }}</li>
        </ul>
        <h4>osc2</h4>
        <ul>
          <li>osc2: {{ osc2 }}</li>
          <li>freq2: {{ freq2 }}</li>
          <li>wave2: {{ wave2 }}</li>
        </ul>
        <h4>Osc3</h4>
        <ul>
          <li>osc3: {{ osc3 }}</li>
          <li>freq3: {{ freq3 }}</li>
          <li>wave3: {{ wave3 }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      playing: false,
      aCtx: null,
      freq1: 261.63,
      freq2: 329.63,
      freq3: 196.0,
      wave1: 'sine',
      wave2: 'sine',
      wave3: 'sine',
      osc1: null,
      osc2: null,
      osc3: null,
      mainGain: 0.01,
      debug: false,
    };
  },
  methods: {
    setupAudio() {
      const AudioContext = window.AudioContext || window.webkitAudioContext;
      this.aCtx = new AudioContext();
    },
    playPause() {
      if (!this.playing) {
        this.playing = true;

        if (this.aCtx == null) {
          const AudioContext = window.AudioContext || window.webkitAudioContext;
          this.aCtx = new AudioContext();
        }

        this.mainGainNode = this.aCtx.createGain();

        this.mainGainNode.gain.value = this.mainGain;
        this.mainGainNode.connect(this.aCtx.destination);

        this.osc1 = this.aCtx.createOscillator();
        this.osc1.frequency.setValueAtTime(this.freq1, this.aCtx.currentTime);
        this.osc1.type = this.wave1;
        this.osc1.connect(this.mainGainNode);
        this.osc1.start();

        this.osc2 = this.aCtx.createOscillator();
        this.osc2.frequency.setValueAtTime(this.freq2, this.aCtx.currentTime);
        this.osc2.type = this.wave2;
        this.osc2.connect(this.mainGainNode);
        this.osc2.start();

        this.osc3 = this.aCtx.createOscillator();
        this.osc3.frequency.setValueAtTime(this.freq3, this.aCtx.currentTime);
        this.osc3.type = this.wave3;
        this.osc3.connect(this.mainGainNode);
        this.osc3.start();
      } else {
        this.playing = false;

        this.osc1.stop();
        this.osc2.stop();
        this.osc3.stop();
      }
    },
    updateFreq1() {
      this.osc1.frequency.value = this.freq1;
    },
    updateFreq2() {
      this.osc2.frequency.value = this.freq2;
    },
    updateFreq3() {
      this.osc3.frequency.value = this.freq3;
    },
    updateWave(id, type) {
      switch (id) {
        case 1:
          this.wave1 = type;
          this.osc1.type = type;
          break;
        case 2:
          this.wave2 = type;
          this.osc2.type = type;
          break;
        case 3:
          this.wave3 = type;
          this.osc3.type = type;
          break;
      }
    },
    setChord(type) {
      switch (type) {
        case 'CMajor':
          this.freq1 = 261.63;
          this.freq2 = 329.63;
          this.freq3 = 196.0;
          break;
        case 'DMajor':
          this.freq1 = 146.83;
          this.freq2 = 185.0;
          this.freq3 = 220.0;
          break;
        case 'EMajor':
          this.freq1 = 164.81;
          this.freq2 = 207.65;
          this.freq3 = 246.94;
          break;
        case 'FMajor':
          this.freq1 = 174.61;
          this.freq2 = 220.0;
          this.freq3 = 130.81;
          break;
        case 'GMajor':
          this.freq1 = 196.0;
          this.freq2 = 246.94;
          this.freq3 = 146.83;
          break;
        case 'AMajor':
          this.freq1 = 220.0;
          this.freq2 = 138.59;
          this.freq3 = 164.81;
          break;
        case 'BMajor':
          this.freq1 = 246.94;
          this.freq2 = 155.56;
          this.freq3 = 185.0;
          break;
      }

      this.updateFreq1();
      this.updateFreq2();
      this.updateFreq3();
    },
    randomFreq() {
      this.freq1 = Math.random() * (1200 - 110) + 110;
      this.freq2 = Math.random() * (1200 - 110) + 110;
      this.freq3 = Math.random() * (1200 - 110) + 110;

      this.updateFreq1();
      this.updateFreq2();
      this.updateFreq3();
    },
  },
};
</script>
