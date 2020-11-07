<template lang="pug">
  header.global-header
    span Header
</template>

<script lang="ts">
  import {Component, Vue} from "~/node_modules/nuxt-property-decorator";

  @Component({})
  export default class GlobalHeader extends Vue {
  }
</script>

<style lang="scss">
  .global-header {
  }

</style>
