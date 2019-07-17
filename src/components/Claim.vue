<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACE</h1>
    <p class="subclaim">Beign your journey throught our amazing galaxy, and discover places you never even heard of.</p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: "Claim"
};
</script>
<style lang="scss">
    .claimWrapper {
        margin-top: 18vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-family: 'Montserrat', sans-serif;
        color: white;
        display: flex;
        flex-wrap: wrap;
    }
    .claim {
        font-size: 50px;
        margin: 0;
        margin-bottom: 40px;
        letter-spacing: 20px;
        text-align: center;
          display: flex;
        flex-wrap: wrap;
    }
    .subclaim {
        font-size: 20px;
        text-align: center;
        max-width: 550px;
        line-height: 1.2;
          display: flex;
        flex-wrap: wrap;
    }
</style>