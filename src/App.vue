<template>
  <Logo />
  <Form />
</template>

<script>
import Form from "./components/Form.vue";
import Logo from "./components/Logo.vue";

export default {
  name: 'App',
  components: { Form, Logo }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
