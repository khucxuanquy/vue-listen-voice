<script>
import Vue from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
import { VueListenVoiceSample } from '@/entry.esm';

export default Vue.extend({
  name: 'ServeDev',
  components: {
   VueListenVoiceSample,
  },
  data(){ return {
    isListen: false,
  }},
   methods: {
    textFromSpeech (text) {
      console.log('textFromSpeech: ', text)
    }
  }
});
</script>

<template>
  <div id="app">
    <vue-listen-voice-sample
      :listen="isListen"
      :language="'vi-VN'"
      @textFromSpeech="textFromSpeech"
    />
    <button
      @click="isListen = !isListen"
      v-text="isListen ? 'stop' : 'start'"
    />
  </div>
</template>
