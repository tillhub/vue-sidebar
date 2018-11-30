<template>
  <div id="app">
    <h1>Main content is here</h1>
    <el-button @click="showSidebar = !showSidebar">toggle sidebar</el-button>
    <el-sidebar
      :visible.sync="showSidebar"
      title="Hello, Sidebar"
      :show-title="false"
      padding="16px">
      <div>
        <h2>Sidebar content is here</h2>
      </div>
      <span slot="footer">
        <el-button @click="showSidebar = false">Close</el-button>
      </span>
    </el-sidebar>
  </div>
</template>

<script>
import ElSidebar from '../src/index.vue'

export default {
  components: {
    ElSidebar
  },
  data () {
    return {
      showSidebar: false
    }
  },
  methods: {
  }
}

</script>

<style>
</style>
