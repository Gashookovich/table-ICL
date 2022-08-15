<template>
  <PageLogs />
  <PageLogs2 class="table2"/>
</template>

<script>
import PageLogs from "@/components/PageLogs";
import PageLogs2 from "@/components/PageLogs";

export default {
  name: 'App',
  components: {
    PageLogs,
    PageLogs2,
  }
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
.table2 {
  padding-top: 50px;
}
</style>
