<template>
    <div>
        <SelectFolder v-on:folder-change="test" />
        <div>
            <FolderViewer v-if="folderInfo" :depth="0" :folderInfo="folderInfo"/>
        </div>
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
    }
  }
}
</script>
