<template>
  <div class="dropdown">
    <h1>Cart</h1>
    <p>Your cart is empty</p>
  </div>
</template>
<script>




</script>
<style scoped>
.dropdown{
     border:1px solid red;
     position:absolute;
     top:5rem;
     width:240px;
     border:1px solid white;
     box-shadow:0px 0px 10px grey;
     border-radius:2px;
     z-index:10;
 }
@media(max-width:768px){
   .dropdown{
     top:5.2rem;
     z-index:10;
     background:white;
     right:0;
     }
    }
h1{
  border-bottom:1px solid grey;
  font-size:16px;
  margin-top:8px;
  padding-left:1rem;
  padding-bottom:0.5rem;
 }
 p{
  text-align:center;
  padding-bottom:1.5rem;
  padding-top:4rem;
  padding-left:2rem;
  padding-right:2rem;
  }

</style>