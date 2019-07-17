<template>
  <div class="searchWrapper">
    <input id="search" name="search" @input="handleChange" :value="value" :class="{ dark: dark }">
  </div>
</template>

<script>


export default {
  name: "SearchInput",
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    }
    
  }
};
</script>


<style lang="scss">
.searchWrapper {
  margin-top: 45px;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  width: 250px;

  input {
    color: white;
    text-align: center;
    text-transform: uppercase;
    font-size: 18px;
    height: 30px;
    border: 0;
    border-bottom: 2px solid white;
    background: none;
    transition: box-shadow .3s ease-in-out;
  }

  input:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.685);
  }

  .dark {
    color: black;
    border-bottom-color: black;
    // margin-top: 43.5vh;
    margin-top: 14vh;
  }  
  .dark:focus {
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
  }
}
</style>