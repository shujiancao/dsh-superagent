<template>
  <div id="app">
    <router-view/>
    <common-footer v-if="showFooter"/>
  </div>
</template>

<script>
import CommonFooter from "@/components/CommonFooter";

export default {
  name: "App",
  components: {
    CommonFooter
  },
  computed: {
    showFooter() {
      return Boolean(this.$route.meta.tab);
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
