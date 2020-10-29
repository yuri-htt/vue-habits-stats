<template>
  <h1>{{ value }}</h1>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class HeaderText extends Vue {
  @Prop() private value!: string;
}
</script>

<style scoped>
h1 {
  size: 32px;
  text-align: left;
}
</style>
