<template>
    <li :style="ident">
        <div class="show" @click="activeChildren">
            <i class="el-icon-document" v-if="!isFolder"></i>
            <i class="el-icon-menu folder" v-if="isFolder"></i>
            <span>{{ name }}</span>
        </div>
        <FolderViewer
            v-for="(file, key) in folderInfo.files"
            v-bind:key="key"
            v-if="isFolder && (isFolder && childrenActive)"
            :depth="depth + 1"
            :folderInfo="file"
            :name="file.name"
            :isFolder="file.isFolder"/>
    </li>
</template>
<script>
export default {
  props: {
    depth: Number,
    folderInfo: Object,
    name: String,
    isFolder: Boolean
  },
  data: function () {
    return {
      childrenActive: false
    }
  },
  name: 'FolderViewer',
  computed: {
    ident: function () {
      let margin = 15 * this.depth
      return `margin-left: ${margin}px`
    }
  },
  methods: {
    activeChildren: function () {
      if (this.isFolder) {
        this.childrenActive = !this.childrenActive
      }
    }
  }
}
</script>

<style lang="scss">
.show {
    width: 100%;
    display: flex;
}
.folder {
    cursor: pointer;
}
</style>
