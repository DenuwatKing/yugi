<template>
  <div>
    <NavTop/>
    <TableCenter/>
</div>
 
</template>
<script>
import NavTop from './components/NavBar.vue'
import TableCenter from './components/Table.vue'

export default {
  name:"app",
  components:{
    NavTop,
    TableCenter,
  },

    data() {
      return {
       
      }
    },
    methods: {
     
    }
  }
</script>
<style>
  
</style>