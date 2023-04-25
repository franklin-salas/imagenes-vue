<template>
  <div>
    <ul ref="imageList">
      <li v-for="(image, index) in images" :key="index" class="image-container">
        <a class="delete-icon" @click="removeImage(index)"><i class="fas fa-times"></i></a>
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
        { id: 1,src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', alt: 'Imagen 1' },
        { id: 2, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 2' },
        { id: 3,src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 3' },
          { id: 4,src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', alt: 'Imagen 4' },
            { id: 5,src: 'https://res.cloudinary.com/milecia/image/upload/v1653756834/wood_vuxmb7.jpg', alt: 'Imagen 5' }, { id: 6, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 6' },
        { id: 7,src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 7' },
         { id: 8, src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 8' },
        { id: 9,src: 'https://res.cloudinary.com/milecia/image/upload/v1652466294/map-shots/c2dhtxam0xkjbd3w5znd.jpg', alt: 'Imagen 9' },
        // Agrega más imágenes aquí
      ],
    };
  },
  mounted() {
    const imageList = this.$refs.imageList;
    this.sortable = new Sortable(imageList, {
      // Opciones de SortableJS aquí

         onEnd: this.onSortEnd,
    });


    // const el = this.$refs.sortable;
    // this.sortable = Sortable.create(el, {
    //   onEnd: this.onSortEnd,
    // });
  },

  methods: {
  removeImage(index) {
    this.images.splice(index, 1);
  },

   onSortEnd(event) {
      const movedItem = this.images.splice(event.oldIndex, 1)[0];
      this.images.splice(event.newIndex, 0, movedItem);
      console.log('antiguo',event.oldIndex)
      console.log('nuevo',event.newIndex)
    },
},

};
</script>

<style scoped>
/* ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
}

li {
  margin: 10px;
  display: flex;
  position: relative;
  border-radius: 15px;
  overflow: hidden;
}

li img {
  width: 100%;
  height: auto;
}

li:first-child img {
  max-width: 360px;
}

li:not(:first-child) img {
  max-width: 160px;
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
} */

</style>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  grid-gap: 10px;
  align-items: start;
}

li {
  display: flex;
  position: relative;
  border-radius: 15px;
  overflow: hidden;
}

li img {
  width: 100%;
  height: auto;
}

li:first-child {
  grid-area: span 2 / span 2;
}

li:first-child img {
  max-width: 100%;
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
</style>
