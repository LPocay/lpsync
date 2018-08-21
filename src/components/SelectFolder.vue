<template>
    <el-row>
        <el-col :span="20">
            <span>{{ folderText }}</span>
        </el-col>
        <el-col :span="4">
            <el-button icon="el-icon-search" circle v-on:click="$refs.folderInput.click()"></el-button>
            <input type="file" name="folder" ref="folderInput" v-on:change="folderChange" hidden webkitdirectory directory>
        </el-col>
    </el-row>
</template>

<script>
import * as fs from 'fs'
import * as path from 'path'

export default {
  data: function () {
    return {
      folder: {
        isFolder: true,
        isReady: false,
        name: '',
        files: []
      },
      count: 0,
      folderText: 'Select Folder'
    }
  },
  methods: {
    folderChange: function (event) {
      if (event.target.files.length > 0) {
        this.folder = {
          isFolder: true,
          isReady: false,
          name: '',
          files: []
        }
        this.readDirectory(event.target.files[0].path, this.folder, () => {
          this.$emit('folder-change', this.folder)
        })
      }
    },
    readDirectory: function (pathFolder, results, complete) {
      this.count++
      fs.readdir(pathFolder, (err, files) => {
        if (err) {
          return err
        }
        let pending = files.length
        files.forEach((file, index) => {
          let filePath = path.resolve(pathFolder, file)
          let fileStats = fs.statSync(filePath)
          if (fileStats.isDirectory()) {
            results.files[index] = {
              isFolder: true,
              isReady: false,
              path: filePath,
              stats: fileStats,
              name: file,
              files: []
            }
            this.readDirectory(filePath, results.files[index], complete)
          } else {
            results.files.push({
              isFolder: false,
              isReady: true,
              path: filePath,
              stats: fileStats,
              name: file
            })
          }
          pending--
          if (!pending) {
            results.isReady = true
          }
        })
        this.count--
        if (this.count === 0 && complete) {
          complete()
        }
      })
    }
  }
}
</script>
