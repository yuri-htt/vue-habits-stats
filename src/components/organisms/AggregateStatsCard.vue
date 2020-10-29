<template>
  <div class="card">
    <div class="heat-map-container">
      <HeatMap
        colorType="forest"
        :values="values"
        :weeksCountForDisplay="24"
        size="small"
      />
    </div>
  </div>
</template>

<script lang="ts">

import dayjs from 'dayjs'
import HeatMap from '../molecules/HeatMap.vue'
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({
  components: {
    HeatMap
  }
})

export default class AggregateAtatsCard extends Vue {
  @Prop({ default: 'forest' }) private colorType!: 'forest' | 'spring' | 'ocean' | 'mican' | 'tomato'
  @Prop({ default: 4 }) private weeksCountForDisplay!: number;
  @Prop() private values!: {[key: string]: number }

  private dateArray: {[key: string]: number }[] = []
  private today!: dayjs.Dayjs
  private startDate!: dayjs.Dayjs

  data () {
    return {
    }
  }
}

</script>

<style scoped>
.card {
  border: 1px solid #EAEAEA;
  box-sizing: border-box;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 4px;
}
.heat-map-container {
  padding: 16px
}
</style>
