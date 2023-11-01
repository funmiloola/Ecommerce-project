<template>
  <div class="sidebar">
    <div class="sidebar-options" v-if="showSidebar">
     <img src="@/assets/images/icon-close.svg" alt="" v-on:click="closeSidebar">
     <nav>
      <ul>
       <li v-for="option in options" v-bind:key="option.id">{{option.name}}</li>
      </ul>
     </nav>
    </div>
  </div>
</template>
<script>
export default {
  props: {
  showSidebar: Boolean,
  closeSidebar: Function 
},
  data() {
    return {
      options:[
              {id:1, name:'Collections'},
              {id:2,name:'Men'},
              {id:3,name:'Women'},
              {id:4,name:'About'},
              {id:5,name:'Contact'}
              ],
    };
  },

};
</script>
<style scoped>
.sidebar-options{
   width:50%;
   height:1000px;
   margin:0;
   display:none;
   position:absolute;
   left:0;
   top:0;
   background:#fff;
   }
img{
   padding-top:16px;
   padding-left:36px;
   }
li{
  margin-top:2rem;
  padding-top:1rem;
  list-style-type:none;
  font-size:24px;
  font-weight:bold;
  }
@media(max-width:768px){
   .sidebar-options{
      display:block;
      }
      }
</style>
