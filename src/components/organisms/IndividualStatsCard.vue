<template>
  <div class="card">
    <p class="title">{{ title }}</p>
    <div class="heat-map-container">
      <HeatMap
        :values="values"
        :colorType="colorType"
        :vertical="true"
        size="regular"
        verical="true"
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

export default class IndividualStatsCard extends Vue {
  @Prop({ default: 'forest' }) private colorType!: 'forest' | 'spring' | 'ocean' | 'mican' | 'tomato'
  @Prop() private values!: {[key: string]: number }
  @Prop() private title!: string

  private weeksCountForDisplay = 4
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
  padding: 16px
}
.title {
  font-size: 16px;
  font-weight: 700;
  text-align: left;
}

.heat-map-container {

}
</style>
