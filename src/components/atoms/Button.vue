<template>
  <button class="button" @click="method" :class="type">
    <slot>
      OK
    </slot>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class Button extends Vue {
  @Prop() onClickAction!: () => void
  @Prop({ default: 'flat' }) type!: 'primary' | 'secondary' | 'flat'

  method () {
    if (!this.onClickAction) {
      console.log('⚠️: No Action Setted!')
    } else {
      this.onClickAction()
    }
  }
}
</script>

<style scoped>
.button {
  background-color: white;
  border: none;
  font-size: 16px;
}

.flat {
  color: #1F95EA;
  font-weight: 700;
}
</style>
