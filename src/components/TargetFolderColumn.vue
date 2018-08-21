<template>
    <el-row>
        <el-col :span="20">
            <span>{{ folderText }}</span>
        </el-col>
        <el-col :span="4">
            <el-button icon="el-icon-search" circle></el-button>
        </el-col>
    </el-row>
</template>

<script>
export default {
  data: function () {
    return {
      folderText: 'Select a folder'
    }
  }
}
</script>
