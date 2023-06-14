<template>
  <div id="app">
    <div>
      <h1>Scan Location</h1>
      <div class="section">
        <QRScanner style="width: 100%" @result="onScan" />
      </div>
      <h3>Items</h3>
      <div v-for="(item, index) in items" :key="index">{{ item }}</div>
      <div>
        {{ result }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import QRScanner from "./components/QRCodeSanner.vue";

const items = ref<string[]>([]);
const result = ref("");
function onScan(decodedText: string) {
  items.value.push(decodedText);
  console.log(decodedText);
}
</script>
