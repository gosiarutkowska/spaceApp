<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="../img/moo.svg" class="logo" v-if="step === 1" @click="step = 0;">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step ===0"/>
    </transition>
    <claim v-if="step===0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
       <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
    </div>
    <Modal v-if="modalOpen" :item="modalItem"  @closeModal="modalOpen = false"/>
  </div>
</template>


<script>
import claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";
import HeroImage from "@/components/HeroImage";
import Item from "@/components/Item";
import Modal from "@/components/Modal"
import axios from "axios";
import debounce from "lodash";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  data() {
    return {
      modalOpen: false,  
      searchValue: "",
      results: [],
      loading: false,
      step: 0,
      modalItem: null,
    };
  },
  components: {
    claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
  methods: {
    handleInput: _.debounce(function(e) {
      this.loading = true;
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
          console.log(response.data.collection.items);
          this.loading = false;
          this.step = 1;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500),
    handleModalOpen(item) {
        this.modalOpen = true;
        this.modalItem = item;
    },
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}

.wrapper {
  margin: 0;
  position: relative;
  width: 100%;
  min-height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  &.flexStart {
    justify-content: flex-start;
  }
}

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 64px;
  height: 64px;

  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
.loader:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s linear infinite;

  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.logo {
  position: absolute;
  top: 30px;
}

.results {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  max-width: 1250px;
  margin: 10px;
  justify-content: center;
  align-items: center;

  
  div {
      margin: 10px;
      border: 5px solid black;
      max-width: 300px;
  }
}
</style>