<template>
  <div>
    <ul ref="imageList">
      <li v-for="(image, index) in images" :key="index">
        <img :src="image.src" :alt="image.alt" />
      </li>
    </ul>
  </div>
</template>
<script>
import Sortable from 'sortablejs';

export default {
  data() {
    return {
      images: [
        { src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', alt: 'Imagen 1' },
        { src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 2' },
        { src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 3' },

           { src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 2' },
        { src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 3' },
          { src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', alt: 'Imagen 1' },
        // Agrega más imágenes aquí
      ],
    };
  },
  mounted() {
    const imageList = this.$refs.imageList;
    this.sortable = new Sortable(imageList, {
      // Opciones de SortableJS aquí
    });
  },
};
</script>
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px;
  display: inline-block;
  border-radius: 15px;
  overflow: hidden;
}

li img {
  width: 100%;
  height: auto;
}

li:first-child img {
  max-width: 300px;
}

li:not(:first-child) img {
  max-width: 200px;
}
</style>
