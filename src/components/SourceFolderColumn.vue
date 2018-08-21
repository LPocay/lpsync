<template>
    <div>
        <SelectFolder v-on:folder-change="test" />
        <el-row>
          <el-col :span="24">
            <ul class="folder-list">
              <FolderViewer
                v-if="folderInfo"
                :depth="0"
                :folderInfo="folderInfo"
                :name="folderInfo.name"
                :isFolder="true"/>
            </ul>
          </el-col>
        </el-row>
    </div>
</template>

<script>
import SelectFolder from './SelectFolder.vue'
import FolderViewer from './FolderViewer.vue'

export default {
  components: {
    SelectFolder,
    FolderViewer
  },
  data: function () {
    return {
      folderInfo: null
    }
  },
  methods: {
    test: function (folder) {
      this.folderInfo = Object.create(folder)
      console.log(this.folderInfo)
    }
  }
}
</script>
<style lang="scss">
.folder-list {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>
