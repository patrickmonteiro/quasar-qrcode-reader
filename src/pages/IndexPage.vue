<template>
  <q-page class="flex flex-center q-pa-md">
    <q-card flat bordered class="reader-card">
      <q-card-section class="text-center">
        <img
          v-if="!showCamera"
          alt="QR code scan"
          src="/qr_code.svg"
          class="reader-card__illustration"
        />

        <div v-else class="reader-card__stream">
          <qrcode-stream @detect="onDetect" @error="onError" />
        </div>

        <p class="text-body2 text-grey-5 q-mt-md q-mb-none">{{ textInfo }}</p>

        <div v-if="result" class="reader-card__result q-mt-sm">
          <q-icon name="check_circle" color="primary" size="18px" class="q-mr-xs" />
          <span class="text-body2 text-grey-3">{{ result }}</span>
        </div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-btn
          v-if="!showCamera"
          unelevated
          no-caps
          color="primary"
          icon="camera_alt"
          label="Read QRCode"
          class="full-width"
          @click="turnCameraOn"
        />
        <q-btn
          v-else
          flat
          no-caps
          color="grey-5"
          label="Cancel"
          class="full-width"
          @click="turnCameraOff"
        />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, computed } from 'vue'
import { QrcodeStream } from 'vue-qrcode-reader'

const result = ref(null)
const showCamera = ref(false)

const textInfo = computed(() =>
  showCamera.value
    ? 'Position the QRCode in front of the camera'
    : 'Press the button and scan a QRCode.',
)

function onDetect(detectedCodes) {
  result.value = detectedCodes[0]?.rawValue ?? null
  turnCameraOff()
}

function onError(error) {
  console.error('[QrcodeStream error]', error)
}

function turnCameraOn() {
  showCamera.value = true
}

function turnCameraOff() {
  showCamera.value = false
}
</script>

<style scoped>
.reader-card {
  width: 100%;
  max-width: 420px;
}

.reader-card__illustration {
  width: 100%;
  max-width: 220px;
}

.reader-card__stream {
  overflow: hidden;
  border-radius: var(--pulsar-border-radius);
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.reader-card__result {
  display: flex;
  align-items: center;
  justify-content: center;
  word-break: break-all;
}
</style>
