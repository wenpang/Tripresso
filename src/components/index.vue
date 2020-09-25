<template>
    <div class="main">
      <!-- 輪播 -->
      <carousel/>
      <navbar/>
    </div>
</template>

<script>
  import Navbar from "./navbar";
  import carousel from "./carousel";

    export default {
        name: "index",
        components: {
          Navbar,
          carousel
        }
    }
</script>

<style scoped>

  @media screen and (min-width: 1280px){

  }
  @media screen and (min-width: 768px) and (max-width: 1279px){

  }
  @media screen and (max-width: 767px){

  }

</style>
