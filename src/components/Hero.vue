<template>
  <div class="relative bg-blue-800 h-80">
    <div class="absolute text-white inset-0">
      <h1 class="py-6 mx-auto w-36 text-xl font-bold whitespace-nowrap">Currency Converter</h1>
      <Converter></Converter>
    </div>
  </div>
</template>

<script>
import Converter from "./Converter.vue"

export default {
  name: "Hero",

  components: {
    Converter,
  },

  data() {
    return {
    }
  },
}
</script>

<style scoped>

</style>