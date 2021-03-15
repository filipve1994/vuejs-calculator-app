<template>
  <div class="home">
    <!--    <img alt="Vue logo" src="../assets/logo.png"/>-->
    <Calculator></Calculator>
    <Calculator2></Calculator2>
  </div>
</template>

<script>
// @ is an alias to /src
import Calculator from "../components/Calculator";
import Calculator2 from "@/components/Calculator2";

export default {
  name: "Home",
  components: {
    Calculator2,
    Calculator
  }
};
</script>
