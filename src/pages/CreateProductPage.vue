<template>
   <TheShopLayout>
      <template #default>
         <h2>Neues Produkt</h2>
      </template>
   </TheShopLayout>
</template>


<script>
import TheShopLayout from "@/layouts/TheShopLayout.vue";

export default {
   name: "CreateProductPage",

   components: {
      TheShopLayout
   }
};
</script>


<style scoped>
</style>