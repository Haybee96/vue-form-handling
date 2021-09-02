<template>
  <div class="h-100">
    <div class="container-fluid h-100">
      <div class="row">
        <div class="logo col-md-3 col-sm-12">
          <h3>Create Account</h3>
        </div>

        <div class="form-col col-md-9 col-sm-12">
          <div
            class="form-wrapper col-md-8 col-sm-12 rounded bg-white shadow py-2 px-5"
          >
            <Form></Form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Form from "./components/Form.vue";
export default {
  name: "App",
  components: {
    Form,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300&display=swap");
#app {
  font-family: "Nunito", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(3, 4, 39, 0.8);
  background-repeat: no-repeat;
  color: white;
  background-position: center;
  min-height: 100vh;
}

.form-col {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
