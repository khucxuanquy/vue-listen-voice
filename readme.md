# Vue-listen-voice

## Install

```bash
npm install vue-listen-voice
```

## Usage

```javascript
import Vue from 'vue'
import VueListenVoice from "vue-listen-voice";

Vue.use(VueListenVoice);

```
```html
<template>
  <div>
    <button
      @click="isListen = !isListen"
      v-text="isListen ? 'stop' : 'start'"
    />

    <vue-listen-voice
      :listen="isListen"
      @textFromSpeech="textFromSpeech"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isListen: false,
    }
  },
  methods: {
    textFromSpeech (text) {
      console.log('textFromSpeech: ', text)
    }
  }
}
</script>
```
---
## Documentation

### Properties

| prop | type | default | Descrtiption |
|---|---|---|---|
| **listen** | Boolean | `false` | Can be used to start recording or stop recording  |
| **language** | String | `en-US` | language to recognize speech. you can check supported languages [here](https://cloud.google.com/speech-to-text/docs/languages) |


### Events

| Event | Return| Descrtiption |
|---|---|--|
| **textFromSpeech**| String | Returns the words that vue-listen-voice hears |

## Issues and features requests
If you find something that doesn't work, or a feature request at [https://github.com/khucxuanquy/vue-listen-voice/issues](https://github.com/khucxuanquy/vue-listen-voice/issues)

