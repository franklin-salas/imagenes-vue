<template>
  <div>
    <div ref="sortable" class="image-list">
      <div
        v-for="(image, index) in images"
        :key="image.id"
        class="sortable-item"
        :style="{ width: image.width, height: image.height }"
      >
        <div class="delete-icon" @click="deleteImage(index)"><i class="fas fa-times"></i></div>
        <img :src="image.src" class="image" @load="onImageLoad($event, index)" />
      </div>
    </div>
    <vue-dropzone
      ref="myVueDropzone"
      :options="dropzoneOptions"
      @vdropzone-success="onDropSuccess"
    >
      <div class="dropzone-message">Arrastra y suelta imágenes aquí</div>
    </vue-dropzone>
  </div>
</template>

<script>
import Sortable from 'sortablejs';
import VueDropzone from 'vue2-dropzone';
import 'vue2-dropzone/dist/vue2Dropzone.min.css';

export default {
  components: {
    VueDropzone,
  },
  data() {
    return {
      images: [
        { id: 1, src: 'https://images.unsplash.com/photo-1519681393784-d120267933ba', width: '40%', height: '100px' },
        { id: 2, src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', width: '20%', height: '200px' },
        { id: 3, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', width: '20%', height: '200px' },
        { id: 4, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', width: '20%', height: '200px' },
        { id: 5, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', width: '20%', height: '200px' },
      ],
      dropzoneOptions: {
        url: '/',
        autoProcessQueue: false,
        uploadMultiple: true,
        maxFiles: 5,
        acceptedFiles: 'image/*',
        dictDefaultMessage: '',
      },
      sortable: null,
    };
  },
  mounted() {
    const el = this.$refs.sortable;
    this.sortable = Sortable.create(el, {
      onEnd: this.onSortEnd,
    });
  },
  methods: {
    onDropSuccess(file) {
      const reader = new FileReader();
      reader.addEventListener('load', () => {
        const img = new Image();
        img.src = reader.result;
        img.onload = () => {
          const width = img.width > img.height ? '20%' : 'calc(40% - 20px)';
          const height = img.width > img.height ? 'auto' : '200px';
          this.images.push({ id: Date.now(), src: reader.result, width, height });
          this.$refs.myVueDropzone.removeAllFiles();
        };
      });
      reader.readAsDataURL(file);
    },
        deleteImage(index) {
      this.images.splice(index, 1);
    },
    onSortEnd(event) {
      const movedItem = this.images.splice(event.oldIndex, 1)[0];
      this.images.splice(event.newIndex, 0, movedItem);
    },
    onImageLoad(event, index) {
      const img = event.target;
      const width = img.width > img.height ? '20%' : 'calc(40% - 20px)';
      const height = img.width > img.height ? 'auto' : '200px';
      this.$set(this.images[index], 'width', width);
      this.$set(this.images[index], 'height', height);
    },
  },
};
</script>

<style>
.image-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.sortable-item {
  display: inline-block;
  margin: 10px;
  position: relative;
  border: 1px solid #ccc;
  border-radius: 10px;
  overflow: hidden;
}

.sortable-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.delete-icon {
  position: absolute;
  top: 5px;
  right: 5px;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  cursor: pointer;
  color: #aaa;
  transition: color 0.2s ease;
}

.delete-icon:hover {
  background-color: rgba(255, 0, 0, 0.8);
  color: #fff;
}

.dropzone-message {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  font-weight: bold;
  padding: 50px;
  border: 2px dashed gray;
  border-radius: 10px;
  cursor: pointer;
  color: gray;
  transition: background-color 0.2s ease;
}

.dropzone-message:hover {
  background-color: #f5f5f5;
}

.vue-dropzone {
  margin: 20px;
}



</style>

