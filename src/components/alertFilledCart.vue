<template>
  <div class="dropdown">
    <h1>Cart</h1>
    <div class="details">
    <img src="@/assets/images/image-product-1-thumbnail.jpg" alt="" id="img" >
    <p>Fall Limited Edition Sneakers <br>
    <span> ${{priceProp}} x {{cartQuantityProp}} <strong> ${{ total() }}</strong> </span> </p>
    <img src="@/assets/images/icon-delete.svg" alt="" id="delete-icon" v-on:click="deleteCart">
    </div>
    <button>Checkout</button>
  </div>
</template>
<script>
export default {
props: {
  priceProp: Number,      
  cartQuantityProp: Number,  
  deleteCart:Function,       
},
 data() {
   return{
   }
  },
  methods:{
    total:function(){
    return  this.priceProp * this.cartQuantityProp;
      }
    }
 }
</script>
<style scoped>
.dropdown{
   border:1px solid white;
   box-shadow:0px 0px 10px grey;
   border-radius:2px;
   position:absolute;
   top:4.5rem;
   width:250px;
   z-index:5;
 }
 @media(max-width:768px){
    .dropdown{
      right:0;
      background:white;
      top:5.2rem;
      }
    }
 h1{
  font-size:16px;
  margin-top:8px;
  padding-left:1rem;
  }
  .details{
    display:flex;
    gap:10px;
    padding-left:20px;
    padding-top:12px;
    padding-right:12px;
    padding-bottom:16px;
    }
    #img{
     width:50px;
     height:45px;
     border-radius:4px;
     }
     p{
       margin-top:-2px;
       font-size:12.5px;
      }
     #delete-icon{
       height:16px;
       transform:translateY(10px);
       }
  button{
      padding-top:6px;
      padding-bottom:6px;
      padding-left:72px;
      padding-right:84px;
      margin-bottom:14px;
      margin-left:24px;
      border-radius:8px;
      background:orange;
      color:white;
      border-color:orange;
      }
</style>