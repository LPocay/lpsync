<template>
    <ul>
        <li v-for="(file, key) in folderInfo.files" v-bind:key="key" v-if="file.isReady">
            <i class="el-icon-document" v-if="!file.isFolder"></i>
            <i class="el-icon-menu" v-if="file.isFolder"></i>
            <span>{{ file.name }}</span>
            <FolderViewer v-if="file.isFolder" :depth="depth + 1" :folderInfo="file" />
        </li>
    </ul>
</template>
<script>
export default {
  props: {
    depth: Number,
    folderInfo: Object
  },
  name: 'FolderViewer'
}
</script>
