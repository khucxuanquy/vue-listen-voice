<template />
<script>
export default {
  props: {
    listen: {
      type: Boolean,
      default() {
        return false
      }
    },
    language: {
      type: String,
      default() {
        return 'en-US'
      }
    }
  },
  data() {
    return {
      text: "",
      runtimeTranscription: "",
    };
  },
  methods: {
    listenVoice() {
      if (!this.listen) return;
      window.recognition && window.recognition.start();
    },

    stopListenVoice() {
      this.text = ''
      window.recognition && window.recognition.stop();
    }
  },
  watch: {
    listen(isListen) {
      isListen === true ? this.listenVoice() : this.stopListenVoice();
    },
    text(txt) {
      if(txt !== '') this.$emit('textFromSpeech', txt)
    }
  },
  mounted() {
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    if (!SpeechRecognition) {
      throw new Error(
        "Speech Recognition does not exist on this browser. Use Chrome or Firefox"
      );
    }
    if (!SpeechRecognition) return;
    const recognition = new SpeechRecognition();
    recognition.interimResults = true;
    // set language
    recognition.lang = this.language

    recognition.addEventListener("result", e => {
      // r result
      const text = Array.from(e.results).map(r => r[0]).map(r => r.transcript).join("");
      this.runtimeTranscription = text;
    });

    recognition.addEventListener("end", () => {
      if (this.runtimeTranscription !== "") this.text += ' ' + this.runtimeTranscription;
      this.runtimeTranscription = "";
      // listen continuously
      this.listenVoice();
    });
    window.recognition = recognition;

    // start listen
    if(this.listen) this.listenVoice()
  },
  beforeDestroy() {
    this.stopListenVoice()
  },
}
</script>