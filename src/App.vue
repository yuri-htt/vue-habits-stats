<template>
  <div id="app">
    <NavigationBar />
    <div class="container">
      <HeaderText value="トータルスタッツ" />
      <AggregateAtatsCard
        colorType="forest"
        :values="values"
      />
      <HeaderText value="個別スタッツ" />
      <div class="card-list">
        <div v-for="habit in habits" :key="habit.title" class="individual-card">
          <IndividualStatsCard
            :values="habit.values"
            :title="habit.title"
            :colorType="habit.colorType"
            :marked="habit.marked"
            :onClickMark="onClickMark"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import 'normalize.css'

import NavigationBar from './components/organisms/NavigationBar.vue'
import HeaderText from './components/atoms/HeaderText.vue'
import AggregateAtatsCard from './components/organisms/AggregateStatsCard.vue'
import IndividualStatsCard from './components/organisms/IndividualStatsCard.vue'

@Component({
  components: {
    NavigationBar,
    HeaderText,
    AggregateAtatsCard,
    IndividualStatsCard
  },

  methods: {
    onClickMark (id: number) {
      return console.log('習慣を実行したことをマーク')
    }
  },

  data () {
    return {
      values: [
        { '2020-10-04': 1 },
        { '2020-10-25': 2 },
        { '2020-10-27': 1 }
      ],
      habits: [
        {
          title: '習慣１',
          colorType: 'spring',
          marked: true,
          values: [
            { '2020-10-04': 1 },
            { '2020-10-14': 2 },
            { '2020-10-15': 2 },
            { '2020-10-25': 2 },
            { '2020-10-26': 1 },
            { '2020-10-29': 2 }
          ]
        },
        {
          title: '習慣２',
          colorType: 'ocean',
          marked: false,
          values: [
            { '2020-10-06': 1 },
            { '2020-10-11': 2 },
            { '2020-10-20': 2 },
            { '2020-10-25': 2 },
            { '2020-10-26': 1 }
          ]
        }
      ]
    }
  }
})
export default class App extends Vue {}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.container {
  padding: 32px;
}
.card-list {
  display: flex;
  margin-bottom: 16px;
}
.card-list:last-child {
  margin-bottom: 0;
}
.individual-card {
  margin-right: 16px;
}
.individual-card:last-child {
  margin-right: 0;
}
</style>
