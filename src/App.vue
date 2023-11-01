<template>
  <div id="app">
    <app-header></app-header>
    
  </div>
</template>

<script>
import headerSection from './components/headerSection.vue';
export default {
  components: {
   'app-header':headerSection,
  },
  data(){
      return{
        images:[require('@/assets/images/image-product-1.jpg'),
      require('@/assets/images/image-product-2.jpg'), 
      require('@/assets/images/image-product-3.jpg'),
      require('@/assets/images/image-product-4.jpg')
],
        }
      },
      methods:{
      
      }
}
</script>

<style scoped>

</style>
