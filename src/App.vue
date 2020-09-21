<template >
  <div id="app" >
  <!-- As a heading -->
  <b-navbar variant="faded" type="light" class="bg-danger">
    <b-navbar-brand tag="h1" class="mb-0 bg-danger"><H1 style="color:white">EMS TRACKING</H1></b-navbar-brand>
  </b-navbar>

  <div class="container">
    <div class="row mt-2">
     <div class="col">
       <Thaipost/>
     </div>
        
      
      
      
    </div>
  </div>
    
</div>
  
</template>

<script>

import Thaipost from './components/Thaipost.vue'
export default {
  name: 'App',
  components: {
    Thaipost
  }
}
</script>

<style>
#app{
  font-family: 'Prompt', sans-serif;

}



</style>
