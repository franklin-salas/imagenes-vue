<template>
  <div>
    <vue-dropzone ref="myVueDropzone" id="dropzone" :options="dropzoneOptions"></vue-dropzone>
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
        headers: { "My-Awesome-Header": "header value" },
         addRemoveLinks: true,
        dictRemoveFile: '<i class="fas fa-times"></i>',
        dictCancelUpload: 'Cancelar'
      }
    } 
  },
  // Dentro de tu componente Vue

mounted() {
  
 

},

  methods: {
    
  }
}
</script>

<style scope>
.vue-dropzone {
  border: 2px dashed #3c8dbc;
  border-radius: 15px;
  padding: 20px;
  background-color: #f5f5f5;
}

.vue-dropzone .dz-preview {
  margin: 10px;
}

/* .vue-dropzone >.dz-preview .dz-details{
   background-color: rgba(255, 255, 255, 0.5);
     border-radius: 15px;
} */

.vue-dropzone>.dz-preview .dz-details{
  background-color: transparent;
  border-radius:15px ;
}



.vue-dropzone >.dz-preview .dz-remove {

 position: absolute;
  top: 5px;
  right: 5px;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  
  font-size: 12px;
  cursor: pointer;
  color: #aaa;
  transition: color 0.2s ease;
  display: inline-block;
  border: none;
  cursor: pointer;
  padding: 0;
  text-decoration: none;
  bottom: auto;
}

.vue-dropzone>.dz-preview .dz-image {
    border-radius: 15px;
   
}
.vue-dropzone .dz-preview .dz-remove:hover {
  border: 2px solid red;

   background-color:red;
  color: #fff;

}



</style>