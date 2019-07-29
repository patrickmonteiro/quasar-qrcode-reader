<template>
  <q-page class="container">
    <div class="row">
      <div class="col-12 q-pt-lg">
        <q-input rounded outlined v-model="text" label="Value" />
      </div>
      <div class="col-12 q-pt-md text-center">
        <qriously :value="text" :size="200" />
      </div>
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
  }
}
</script>
