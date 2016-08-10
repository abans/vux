<template>
  <div>
    <img src="../assets/demo/filter_bg.jpg" style="width: 100%">
    <search no-results="meiyou" show-badge placeholder="请选择学校" @result-click="resultClick" @on-change="getResult" :results="results" :show.sync="show" :value.sync="value"></search>
  </div>
  <button @click='showSearch'>show search bar</button>
</template>

<script>
import { Search } from '../components'

export default {
  components: {
    Search
  },
  methods: {
    showSearch () {
      this.show = true
    },
    resultClick (item) {
    },
    getResult (val) {
      this.results = getResult(this.value)
    }
  },
  data () {
    return {
      results: [],
      value: '',
      show: false
    }
  }
}

function getResult (val) {
  let rs = []
  for (let i = 0; i < 40; i++) {
    rs.push({
      title: `${val} result: ${i + 1} `,
      other: i
    })
  }
  if (val === 'aaa') {
    rs = null
  }
  return rs
}
</script>
