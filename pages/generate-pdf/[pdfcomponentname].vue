<template>
  <div>
    <div id="pdf-content">
      <SimpleTable v-if="componentName === 'table'" />
      <SimpleCard v-if="componentName === 'card'" />
    </div>
    <div class="container my-4">
      <button class="btn btn-primary" @click="generatePDF">Generate PDF</button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'

// Get the dynamic component name from route param
const route = useRoute()
const componentName = computed(() => route.params.pdfcomponentname)

const generatePDF = async () => {
  // Only run in browser
  if (process.client) {
    const html2pdf = (await import('html2pdf.js')).default
    const element = document.getElementById('pdf-content')

    if (!element) return

    const opt = {
      margin: 0.5,
      filename: `${componentName.value}-document.pdf`,
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 2 },
      jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
    }

    html2pdf().set(opt).from(element).save()
  }
}
</script>
