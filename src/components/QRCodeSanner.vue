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
  //Start scanning QR codes or bar codes for a given camera
  const config = {
    fps: 1,
    qrbox: { width: 350, height: 350 },
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
  //Stops streaming QR Code video and scanning.
  html5Qrcode?.stop();
}
function pause() {
  //Pauses the ongoing scan
  html5Qrcode?.pause(true);
}
function resume() {
  //Resumes the paused scan.
  html5Qrcode?.resume();
}
function clear() {
  /*
    Clears the existing canvas.  
    Note: in case of ongoing web cam based scan, it needs to be explicitly closed before calling this method, else it will throw exception.
    */
  html5Qrcode?.clear();
}
</script>
