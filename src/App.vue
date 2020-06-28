<template>
  <div>
    <navbar />
    <br />
    <Meals />
    
  </div>
</template>
<script>
import Meals from "./components/Meals";
import navbar from "./components/navbar"
export default {
  name: "App",
  components: {
    Meals,
    navbar
  },
};
</script>
<style>