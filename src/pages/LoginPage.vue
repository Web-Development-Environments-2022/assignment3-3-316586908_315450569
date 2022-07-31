<template>
  <div>
    <div class="imgD">
    <LoginComponent style="margin-top:150px"></LoginComponent>
    </div>
  </div>
</template>

<script>
import LoginComponent from "../components/LoginComponent";
export default {
components: { LoginComponent },
}
</script>

<style>
.imgD {

  background-image: url("../images/recipesImages/img5C.jpg"); /* The image used */
  background-color: #cccccc; /* Used if the image is unavailable */
  height: 400px; /* You must set a specified height */
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover; /* Resize the background image to cover the entire container */
}
</style>