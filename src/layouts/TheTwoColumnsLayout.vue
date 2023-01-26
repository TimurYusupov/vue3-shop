<template>
   <div class="container-fluid" :class="containerClasses">
      <div class="row" :class="rowClasses">
         <div :class="leftColumnClasses">
            <slot name="leftCol">
               <h1>Linke Spalte</h1>
            </slot>
         </div>

         <div :class="rightColumnClasses">
            <slot name="rightCol">
               <h1>Rechte Spalte</h1>
            </slot>
         </div>
      </div>
   </div>
</template>


<script>
export default {
   name: "TheTwoColumnsLayout",

   props: {
      leftColumnClass: {
         type: String,
         default: "col-md-8",
      },
      rightColumnClass: {
         type: String,
         default: "col-md-4"
      },
      fullsize: {
         type: Boolean,
         default: false
      }
   },

   computed: {
      containerClasses() {
         return [this.fullsize ? "vh-100" : ""]; // vh-100 : 100% von dem sichtbaren Bereich des Browsers
      },
      rowClasses() {
         return [this.fullsize ? "h-100" : ""]; // height 100%
      },
      leftColumnClasses() {
         return [this.leftColumnClass, this.fullsize ? "h-100" : ""];
      },
      rightColumnClasses() {
         return [this.rightColumnClass, this.fullsize ? "h-100" : ""];
      }
   }
};
</script>


<style scoped>
</style>