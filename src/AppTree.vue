<template>
  <div>
    <vue-dropzone ref="myVueDropzone" id="dropzone" :options="dropzoneOptions" class="vue-dropzone"></vue-dropzone>
  </div>
</template>

<script>
import vue2Dropzone from 'vue2-dropzone'
import 'vue2-dropzone/dist/vue2Dropzone.min.css'

export default {
  components: {
    vueDropzone: vue2Dropzone
  },
  data() {
    return {
      dropzoneOptions: {
        url: 'http://your-upload-endpoint.com',
        thumbnailWidth: 150,
        maxFilesize: 2,
        headers: { "My-Awesome-Header": "header value" }
      }
    }
  }
}
</script>

<style>
.vue-dropzone {
  border: 2px dashed #3c8dbc;
  border-radius: 10px;
  padding: 20px;
  background-color: #f5f5f5;
}

.vue-dropzone .dz-preview {
  margin: 10px;
}

.vue-dropzone .dz-preview .dz-image img {
  width: 100%;
  height: auto;
  border-radius: 5px;
}
</style>
