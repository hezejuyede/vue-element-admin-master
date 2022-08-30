<template>
  <div class="visibleDiv">
    <div id="enterpriseBar" :style="{width: '100%', height: '300px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'modal',
  data() {
    return {}
  },
  mounted() {
    this.getList()
  },
  created() {
  },
  methods: {
    getList() {
    }
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
