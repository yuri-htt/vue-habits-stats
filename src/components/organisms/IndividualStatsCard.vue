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
    <div v-if="!marked" class="button-container">
      <Button  :onClick="onClickMark" type="flat">
        やったよ！
      </Button>
    </div>
  </div>
</template>

<script lang="ts">
import dayjs from 'dayjs'
import { Component, Prop, Vue } from 'vue-property-decorator'
import HeatMap from '../molecules/HeatMap.vue'
import Button from '../atoms/Button.vue'

@Component({
  components: {
    HeatMap,
    Button
  }
})

export default class IndividualStatsCard extends Vue {
  @Prop({ default: 'forest' }) private colorType!: 'forest' | 'spring' | 'ocean' | 'mican' | 'tomato'
  @Prop() private values!: {[key: string]: number }
  @Prop() private title!: string
  @Prop() private onClickMark!: (id: number) => void
  @Prop({ default: false }) private marked!: boolean

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
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.title {
  font-size: 16px;
  font-weight: 700;
  text-align: left;
}
.heat-map-container {

}
.button-container {
  margin: 8px 0px 0px 0px
}
</style>
