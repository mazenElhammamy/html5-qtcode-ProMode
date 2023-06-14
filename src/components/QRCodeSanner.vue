<template>
  <div id="reader"></div>
  <button @click="start">start</button>
  <button @click="stop">stop</button>
  <button @click="pause">pause</button>
  <button @click="resume">resume</button>
  <button @click="clear" :disabled="true">clear</button>
</template>

<script setup lang="ts">
// import { onMounted } from "vue";
import { Html5Qrcode } from "html5-qrcode";

const emit = defineEmits(["result"]);
let html5Qrcode: Html5Qrcode | null;

const onScanSuccess = (decodedText: string) => {
  emit("result", decodedText);
};
function start() {
  const config = {
    fps: 10,
    qrbox: { width: 250, height: 250 },
  };

  html5Qrcode = new Html5Qrcode(
    "reader" // ID of the element to render the scanner
  );

  html5Qrcode.start(
    { facingMode: "environment" },
    config,
    onScanSuccess,
    () => {}
  );
}
function stop() {
  html5Qrcode?.stop();
}
function pause() {
  html5Qrcode?.pause(true);
}
function resume() {
  html5Qrcode?.resume();
}
function clear() {
  html5Qrcode?.clear();
}
</script>
