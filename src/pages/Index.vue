<template>
  <q-page class="row full-height items-center">
    <div class="col text-center">
      <span class="text-subtitle1 text-grey-9">Press the button and scan a qrcode.</span>
      <q-btn color="blue-grey-10" rounded icon="camera_alt" label="Read QRCode"
        class="full-width" size="lg" @click="turnCameraOn()"
        v-show="!showCamera"/>

        <p class="text-subtitle1" v-if="result">Last result: <b>{{ result }}</b></p>
        <div v-if="showCamera">

          <qrcode-stream :camera="camera" @decode="onDecode">
          </qrcode-stream>
        </div>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
import { QrcodeStream } from 'vue-qrcode-reader'
export default {
  name: 'PageIndex',
  components: { QrcodeStream },
  data () {
    return {
      isValid: undefined,
      camera: 'auto',
      result: null,
      showCamera: false
    }
  },
  methods: {
    async onDecode (content) {
      this.result = content
      this.turnCameraOff()
    },

    turnCameraOn () {
      this.camera = 'auto'
      this.showCamera = true
    },

    turnCameraOff () {
      this.camera = 'off'
      this.showCamera = false
    }
  }
}
</script>

<style scoped>
.validation-success,
.validation-failure,
.validation-pending {
  position: absolute;
  width: 100%;
  height: 100%;

  background-color: rgba(255, 255, 255, .8);
  text-align: center;
  font-weight: bold;
  font-size: 1.4rem;
  padding: 10px;

  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
}
.validation-success {
  color: green;
}
.validation-failure {
  color: red;
}
</style>
