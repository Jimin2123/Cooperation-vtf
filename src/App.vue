<template>
  <default-layout />
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import DefaultLayout from '@/components/layouts/default.vue'

@Component({
  components: {
    DefaultLayout
  }
})
export default class App extends Vue {

}
</script>

<style scoped>

</style>
