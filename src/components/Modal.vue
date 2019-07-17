<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo">
      </div>
      <br>
      <h2 class="title">{{ title }}</h2>
      <br>
      <p class="description">{{ description }}</p>
    </div>
    <div class="close" @click="$emit('closeModal')"></div>
  </div>
</template>


<script>
export default {
  name: "Modal",
  props: {
      item: {
          type: Object,
          required: true,
      }
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 300);
  }
};
</script>

<style lang="scss" >
    *{
        // border: 1px solid green;
    }


  .outerWrapper {
    background: #f6f6f6;
    max-width: 650px;
    height: 500px;
    position: fixed;
    display: flex;
    flex-direction: column;
    flex-wrap:wrap;
  }

  .close {
    position: absolute;
    width: 30px;
    height: 30px;
    padding: 30px;
    right: 0;
    top: 0;
    cursor: pointer;

    &::before,
    &::after {
      position: absolute;
      top: 30px;
      right: 20px;
      content: '';
      width: 20px;
      height: 2px;
      background: black;
      display: block;
    }

    &::before {
      transform: rotate(45deg);
    }

    &::after {
      transform: rotate(-45deg);
    }
  }

  .innerWrapper {
    display: flex;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    .photo {
      
      height: auto;
      width: auto;

      img {
        max-width: 200px;
      }
    }

    .description {
      color: #333;
    }

    .title {
       color: #1e3d4a;
    }
  }
</style>