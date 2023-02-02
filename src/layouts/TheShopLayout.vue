<template>
   <div>
      <Navbar />
      <main>
         <div class="container">
            <div class="row">
               <div class="col-12">
                  <slot>
                     <h1>Hauptbereich</h1>
                  </slot>
               </div>
            </div>
         </div>
      </main>
   </div>
</template>


<script>
import Navbar from "@/components/Navbar.vue";

export default {
   name: "TheShopLayout",
   
   components: {
      Navbar
   }
}
</script>


<style scoped>
</style>