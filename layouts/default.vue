<template>
  <div>
    <Header></Header>
    <nuxt />
  </div>
</template>

<script>
import Header from '@/components/header.vue'
export default {
  components: {
    Header
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
ul,li,ol{
  list-style: none;
}
a{
  text-decoration: none;
  color:inherit;
}
em,i{
  font-style: normal;
}
</style>
