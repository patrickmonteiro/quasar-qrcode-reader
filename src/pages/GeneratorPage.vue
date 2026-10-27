<template>
  <q-page class="flex flex-center q-pa-md">
    <q-card flat bordered class="generator-card">
      <q-card-section>
        <p class="text-body2 text-grey-5 text-center q-mb-md">
          Enter the text you want to insert into your custom QRCode.
        </p>

        <q-input v-model="text" dense outlined label="Value" />
      </q-card-section>

      <q-card-section class="text-center q-pt-none">
        <div class="generator-card__preview">
          <qrcode-canvas ref="qrCanvas" :value="text" :size="200" />
        </div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-btn
          unelevated
          no-caps
          color="primary"
          icon="download"
          label="Download"
          class="full-width"
          @click="downloadCanvas"
        />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { QrcodeCanvas } from 'qrcode.vue'

const text = ref('https://github.com/patrickmonteiro')
const qrCanvas = ref(null)

function downloadCanvas() {
  const canvas = qrCanvas.value?.$el
  if (!(canvas instanceof HTMLCanvasElement)) return

  const link = document.createElement('a')
  link.download = 'QRCode.png'
  link.href = canvas.toDataURL()
  link.click()
}
</script>

<style scoped>
.generator-card {
  width: 100%;
  max-width: 420px;
}

.generator-card__preview {
  display: inline-flex;
  padding: 16px;
  background: #fff;
  border-radius: var(--pulsar-border-radius);
}
</style>
