<template>
  <table-insure-file></table-insure-file>
</template>

<script>
import {defineComponent, defineAsyncComponent,ref} from 'vue';

export default defineComponent({
  name: "Tables",
  components: {
    TableInsureFile: defineAsyncComponent(() => import('components/tables/TableInsureFile')),
  },
  setup() {
    return {
    }
  }
})
</script>

<style>

</style>
