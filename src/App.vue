<template>
  <Main />
  <footer class="footer footerspan">
      <div class="content has-text-centered">
        <p>2021 Underscore-rize</p>
        <p>by Hisokage</p>
      </div>
  </footer>
</template>

<script>
import Main from "./components/Main";

export default {
  name: "App",
  components: {
    Main
  },
};
</script>

<style>
.footer {
  background: #e69138;
  color: #fff;
}
</style>
