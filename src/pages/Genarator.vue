<template>
  <q-page class="container">
    <div class="row justify-center">
      <div class="col-12 q-pt-lg text-center text-blue-grey-9">
        <span class="text-subtitle1">
          Enter the String you want to insert into your custom QRCode.
        </span>
      </div>
      <div class="col-10 q-pt-lg">
        <q-input rounded outlined v-model="text" label="Value" />
      </div>
      <div class="col-12 q-pt-md text-center">
        <qriously :value="text" :size="230" />
      </div>
      <q-btn
        color="blue-grey-10"
        outline
        label="Donwload"
        @click="donwloadCanvas"
      />
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Generator',
  data () {
    return {
      text: 'https://github.com/patrickmonteiro'
    }
  },
  methods: {
    donwloadCanvas () {
      const canvas = document.getElementsByTagName('canvas')
      const link = document.createElement('a')
      link.download = 'QRCode.png'
      link.href = canvas[0].toDataURL()
      link.click()
    }
  }
}
</script>
