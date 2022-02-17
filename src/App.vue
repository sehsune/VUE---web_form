<template>
  <div class="App">
    <SignUpForm />
  </div>
</template>

<script>
import SignUpForm from "./components/SignUpForm.vue";
export default {
  name: "App",
  components: {
    SignUpForm,
  },
};
</script>

<style>
.App {
  text-align: center;
}
body {
  background-color: #eee;
  margin: 0;
}
</style>
