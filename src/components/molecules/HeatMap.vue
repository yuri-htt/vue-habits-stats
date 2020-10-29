<template>
  <div
    style="display:flex"
    :style="[isVericalContainer(vertical)]"
  >
    <div
      v-for="(week, weekIndex) in weeksCountForDisplay"
      :key="weekIndex"
      :style="[isVerical(vertical)]"
    >
      <div
        v-for="(date, dateIndex) in 7"
        :key="dateIndex"
        :style="[dateBoxColor(dateIndex, weekIndex), dateBoxSize(size)]"
      />
    </div>
  </div>
</template>

<script lang="ts">

import dayjs from 'dayjs'

import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class HeatMap extends Vue {
  @Prop({ default: 'forest' }) private colorType!: 'forest' | 'spring' | 'ocean' | 'yugure' | 'greentea'
  @Prop({ default: 4 }) private weeksCountForDisplay!: number
  @Prop() private values!: {[key: string]: number }
  @Prop({ default: false }) private vertical!: boolean
  @Prop({ default: 'regular' }) private size!: 'small' | 'regular'

  private dateArray: {[key: string]: number }[] = []
  private today!: dayjs.Dayjs
  private startDate!: dayjs.Dayjs

  private colorPalette = {
    forest: ['rgba(57, 163, 186, 0.5)', 'rgba(57, 163, 186, 1)'],
    spring: ['rgba(255, 99, 211, 0.5)', 'rgba(255, 99, 211, 1)'],
    ocean: ['rgba(107, 179, 246, 0.5)', 'rgba(107, 179, 246, 1)'],
    yugure: ['rgba(253, 70, 70, 0.5)', 'rgba(253, 70,70, 1)'],
    greentea: ['rgba(45, 173, 110, 0.5)', 'rgba(45, 173, 110, 1)']
  }

  data () {
    return {
      isVericalContainer: (vertical: boolean) => {
        if (vertical) {
          return {
            flexDirection: 'column'
          }
        }
      },
      isVerical: (vertical: boolean) => {
        if (vertical) {
          return {
            display: 'flex'
          }
        }
      },

      dateBoxColor: (i: number, n: number) => {
        const index = i + (7 * n)
        const key = this.startDate.add(index, 'day').format('YYYY-MM-DD')

        // @ts-ignore
        if (this.dateArray[key] === 2) {
          return {
            // @ts-ignore
            backgroundColor: this.colorPalette[this.colorType][1]
          }
        }

        // @ts-ignore
        if (this.dateArray[key] === 1) {
          return {
            // @ts-ignore
            backgroundColor: this.colorPalette[this.colorType][0]
          }
        }

        return {
          backgroundColor: '#EBEBEB'
        }
      },

      dateBoxSize: (size: string) => {
        switch (size) {
          case 'small': {
            return {
              width: '16px',
              height: '16px',
              margin: '1px',
              borderRadius: '2px'
            }
          }
          case 'regular': {
            return {
              width: '20px',
              height: '20px',
              margin: '1px',
              borderRadius: '2px'
            }
          }
        }
      }
    }
  }

  created () {
    const dayOfWeek = dayjs().day()

    // startDate(指定された週数前の日曜日の日付)を算出
    // Ex) 今日:10月27日(火) ４週前の開始日: 10月4日(日)
    const dateOfThisSunday = dayjs().subtract(dayOfWeek, 'day')
    this.startDate = dateOfThisSunday.subtract(this.weeksCountForDisplay - 1, 'week')

    this.today = dayjs()
    const diff = this.today.diff(this.startDate, 'day') + 1

    // MEMO: Vueでは配列が[__ob__: Observer]の形式で返却されるため、JSONパース処理が必要
    const parsedValues = JSON.parse(JSON.stringify(this.values))
    parsedValues.forEach((el: any) => {
      const key = Object.keys(el)[0]
      const value = Object.values(el)[0]
      // @ts-ignore
      this.dateArray[key] = value
    })

    Array(diff)
      .fill(null)
      .forEach((a, i) => {
        const key: string = this.startDate.add(i, 'day').format('YYYY-MM-DD')
        // @ts-ignore
        if (!this.dateArray[key]) {
        // @ts-ignore
          this.dateArray[key] = 0
        }
      })
  }
}
</script>

<style scoped>
:root {
  --test: 'red'
}
</style>
