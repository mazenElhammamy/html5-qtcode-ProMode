<template>
  <div id="app">
    <div>
      <h1>Scan Location</h1>
      <div class="section">
        <QRScanner
          v-bind:qrbox="250"
          v-bind:fps="10"
          style="width: 100%"
          @result="onScan"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import QRScanner from "./components/QRCodeSanner.vue";

function onScan(decodedText: string) {
  console.log(decodedText);
}
</script>
