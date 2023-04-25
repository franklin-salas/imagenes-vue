<template>
  <div class="my-dropzone">
    <vue2-dropzone
      ref="myVue2Dropzone"
      id="myVue2Dropzone"
      :options="dropzoneOptions"
      @vdropzone-queue-complete="onQueueComplete"
    ></vue2-dropzone>
    <div class="file-preview-container">
      <div v-for="file in files" :key="file.id" class="file-preview">
        <div class="file-info">{{ file.name }} ({{ formatFileSize(file.size) }})</div>
        <div class="file-actions">
          <button class="delete-button" @click="deleteFile(file)">
            <i class="fa fa-trash"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'dropzone/dist/dropzone.css'
import 'dropzone/dist/basic.css'
import Vue2Dropzone from 'vue2-dropzone';

export default {
  name: 'MyComponent',
  components: {
    Vue2Dropzone,
  },
  data() {
    return {
      files: [],
      c: {
        url: '/upload',
        autoProcessQueue: true,
        maxFilesize: 10,
        acceptedFiles: 'image/*',
      },
    };
  },
  methods: {
    onQueueComplete() {
      // Handle upload completion
    },
    deleteFile() {
      // Handle file deletion
    },
    formatFileSize(size) {
      const units = ['B', 'KB', 'MB', 'GB', 'TB'];
      let unitIndex = 0;
      while (size >= 1024 && unitIndex < units.length - 1) {
        size /= 1024;
        unitIndex++;
      }
      return `${size.toFixed(2)} ${units[unitIndex]}`;
    },
  },
};
</script>


<style >
.my-dropzone {
  position: relative;
  width: 100%;
  height: auto ;
  min-height: 300px;
  border: 2px dashed #ccc;
  border-radius: 5px;
  background-color: #f8f8f8;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  color: #999;
  margin: 20px 0;
}


.dropzone-previews .dz-preview {
  position: relative;
  display: inline-block;
  width: 150px;
  margin: 10px;
  border: 1px solid #ccc;
  padding: 10px;
  background-color: #fff;
}

.file-preview {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-right: 10px;
  margin-bottom: 10px;
  width: 100px;
  height: 100px;
  background-color: #333;
  color: #fff;
  font-size: 14px;
  border-radius: 10px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  transition: box-shadow 0.3s ease;
}

.file-preview:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.file-info {
  text-align: center;
  margin-top: 10px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.file-actions {
  margin-top: 5px;
  display: flex;
  justify-content: center;
}

.delete-button {
  background-color: #e74c3c;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.delete-button:hover {
  background-color: #c0392b;
}
</style>
