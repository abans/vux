<template>
  <div>
    <img src="../assets/demo/filter_bg.jpg" style="width: 100%">
    <search placeholder="请选择学校" @result-click="resultClick" @on-change="getResult" :results="results" :value.sync="value"></search>
  </div>
</template>

<script>
import { Search } from '../components'

export default {
  components: {
    Search
  },
  methods: {
    resultClick (item) {
    },
    getResult (val) {
      this.results = getResult(this.value)
    }
  },
  data () {
    return {
      results: [],
      value: ''
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
  return rs
}
</script>
