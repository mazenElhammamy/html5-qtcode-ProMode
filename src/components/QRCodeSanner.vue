<template>
  <div id="reader"></div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import { Html5Qrcode } from "html5-qrcode";

const emit = defineEmits(["result"]);
let html5Qrcode: Html5Qrcode | null;

const onScanSuccess = (decodedText: string) => {
  emit("result", decodedText);
};

onMounted(() => {
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
});
</script>
