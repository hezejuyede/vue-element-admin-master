<template>
  <div class="visibleDiv"></div>
</template>

<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      tableData: [
        { 'text': '增加值总总额（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '劳动者报酬（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '固定资产折旧（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '增加值总总额（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '生产税净值（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '营业余额（万元）', 'tb': '2%', 'hb': '4%' }
      ],
    }
  },
  mounted() {
    this.getList()
  },
  created() {
  },
  methods: {
    getList() {
    },
  },
  props: {}
}
</script>
<style lang="scss" scoped>

.visibleDiv {
  width: 100%;
  background-color: #ffffff;
}

</style>

