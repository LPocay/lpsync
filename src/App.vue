<template>
  <div id="app">
    <el-container>
      <el-header>
        <Header />
      </el-header>
      <el-main>
        <el-row>
          <el-col :span="12"><SourceFolderColumn /></el-col>
          <el-col :span="12"><TargetFolderColumn /></el-col>
        </el-row>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import SourceFolderColumn from './components/SourceFolderColumn.vue'
import TargetFolderColumn from './components/TargetFolderColumn.vue'

export default {
  name: 'app',
  components: {
    Header,
    SourceFolderColumn,
    TargetFolderColumn
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}
</style>
