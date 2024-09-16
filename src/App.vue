<script setup>
import { ref } from "vue";
const inputData = ref("");
const csvRows = ref([]);

const convertToCSV = () => {
  const lines = inputData.value.trim().split("\n");
  let currentLabel = "";
  const rows = [];

  // Iterate through each line
  lines.forEach((line) => {
    // Check if the line is a label
    if (
      [
        "Qualcomm相關新聞",
        "MediaTek相關新聞",
        "無線通訊市場",
        "智慧型手機/消費性電子產品",
        "其他業界重要訊息",
      ].includes(line)
    ) {
      currentLabel = line;
    } else {
      // If the line is not empty and not a label, add it to rows
      if (line.trim() !== "" && line.trim() !== "N/A") {
        rows.push({
          text: line,
          label: currentLabel,
        });
      }
    }
  });

  csvRows.value = rows;
};
</script>

<template>
  <div>
    <textarea
      v-model="inputData"
      placeholder="Paste your data here..."
      rows="20"
      cols="80"
    ></textarea>
    <button @click="convertToCSV">Convert to CSV</button>

    <div v-if="csvRows.length > 0">
      <h3>CSV Preview</h3>
  
    
          <div v-for="(row, index) in csvRows" :key="index">
            <p>"{{ row.text }}","{{ row.label }}"</p>
          </div>
      
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
