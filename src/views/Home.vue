<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div class="recognition">
      <button class="record-btn" @click="record">{{ recordBtnValue }}</button>
      <div>
        <textarea class="recorded-text" v-model="recoredText" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue";

@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  msg: string = "こんちは！！";
  recognizing: boolean = false;
  recognition: any = null;
  recordBtnValue = "録音";
  recoredText: string = "";

  async created() {
    const { webkitSpeechRecognition } = window as any;
    const recognition = new webkitSpeechRecognition();
    recognition.lang = "ja-JP";
    recognition.continuous = true;
    recognition.onresult = await this.recognize;
    this.recognition = recognition;
  }

  protected record() {
    if (this.recognizing) {
      this.recognition.stop();
      this.recordBtnValue = "録音";
    } else {
      this.recognition.start();
      this.recordBtnValue = "停止";
    }
    this.recognizing = !this.recognizing;
  }

  protected async recognize(e: SpeechRecognitionEvent) {
    this.recoredText += `${e.results[e.results.length - 1][0].transcript}\n`;
  }
}
</script>
<style lang="scss" scoped>
.home {
  .recognition {
    .recorded-text {
      width: 300px;
      height: 7rem;
      line-height: 1.5em;
    }
  }
}
</style>
