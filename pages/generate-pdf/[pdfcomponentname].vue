<template>
  <div>
    <div id="pdf-content">
      <component :is="selectedComponent" v-if="componentExists" />
      <div v-else class="alert alert-danger">
        Component "{{ componentName }}" not found
      </div>
    </div>
    <div class="container my-4">
      <button class="btn btn-primary" @click="generatePDF" v-if="componentExists">
        Generate PDF
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import SimpleCard from '~/components/SimpleCard.vue'
import SimpleTable from '~/components/SimpleTable.vue'
import test from '~/components/test.vue'

// Available components map
const components = {
  SimpleCard,
  SimpleTable,
  test
}

// Get the dynamic component name from route param
const route = useRoute()
const componentName = computed(() => route.params.pdfcomponentname)

// Check if component exists and get it
const componentExists = computed(() => componentName.value in components)
const selectedComponent = computed(() => components[componentName.value])

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
