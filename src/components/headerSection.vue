<template>
  <div id="main">
    <header>
    <nav>
            <ul class="nav-section">
                <sidebar :showSidebar = "showSidebar" :closeSidebar = "closeSidebar"></sidebar>
                <icon-component :showIcon="showIcon" :displaySidebar="displaySidebar"></icon-component>
                <li><img src="@/assets/images/logo.svg" alt="logo" id="logo"></li>
                <li class="options" v-for="option in options" v-bind:key="option.id">{{option.name}}</li>
            </ul>
            <ul class="nav-section">
                <filled-cart v-if="showFilledAlert" :priceProp = "price" :cartQuantityProp = "cartQuantity" :deleteCart = "deleteCart"></filled-cart>
                 <empty-cart v-if="showEmptyAlert"></empty-cart>
                <li><img src="@/assets/images/icon-cart.svg" alt="cart-icon" id="cart-icn" v-on:click="cartdetails" >
                <span class="badge" v-if="cartQuantity > 0">{{cartQuantity}}</span> </li>
                <li><img src="@/assets/images/image-avatar.png" alt="profile-pic" id="profile-pic" class="profile-pic"></li>
            </ul>
    </nav>
   </header>
     <section class="orders">
    <div>
        <img :src="imageProduct" alt="image-product1" id="img-product">
        <div class="image-products">
            <img src="@/assets/images/image-product-1-thumbnail.jpg" alt="" class="img-product" v-on:click="firstImage">
            <img src="@/assets/images/image-product-2-thumbnail.jpg" alt="" class="img-product" v-on:click="secondImage">
            <img src="@/assets/images/image-product-3-thumbnail.jpg" alt="" class="img-product" v-on:click="thirdImage">
            <img src="@/assets/images/image-product-4-thumbnail.jpg" alt="" class="img-product" v-on:click="fourthImage">
        </div>
    </div>
    <div class="orders-details">
        <h1>{{title}}</h1>
        <h2>{{content}}</h2>
        <p>{{contents}}</p>
        <h3>${{price}}.00    <span>50%</span> </h3>
        <p id="normal-price">$250.00</p>  
        <div>
            <div class="cart-section"> 
        <div class="add-cart">
            <img src="@/assets/images/icon-minus.svg" alt="" v-on:click="subtract(1)" id="icon-minus">
            <strong>{{quantity}}</strong>
            <img src="@/assets/images/icon-plus.svg" alt="" v-on:click="add(1)" id="icon-plus">
        </div>
        <div class="cart">
            <button v-on:click="addToCart"><img src="@/assets/images/icon-cart.svg" alt="cart-icon" id="cart-icon" > Add to cart</button>
        </div>
    </div>
    </div>
    </div>
   </section>
  </div>
</template>

<script>
import sideBar from '@/components/sideBar.vue';
import iconSection from '@/components/iconSection.vue';
import alertFilledCart from '@/components/alertFilledCart.vue';
import alertEmptyCart from '@/components/alertEmptyCart.vue';
export default {
  components: {
      'sidebar':sideBar,
      'icon-component':iconSection,
      'filled-cart':alertFilledCart,
      'empty-cart':alertEmptyCart,
  },
  data(){
  return{
  
  imageProduct:require("@/assets/images/image-product-1.jpg"),
   options:[
              {id:1, name:'Collections'},
              {id:2,name:'Men'},
              {id:3,name:'Women'},
              {id:4,name:'About'},
              {id:5,name:'Contact'}
              ],
         title:'SNEAKERS COMPANY',
         content:'Fall Limited Edition Sneakers',
         contents:'These low-profile sneakers are your perfect casual wear companion.Featuring a durable rubber outer sole,theyll withstand everything the weather can offer.',
         price:125.00,
         quantity:0,
         cartQuantity:0,
         showIcon:false,
         showSidebar:false,
         showFilledAlert:false,
         showEmptyAlert:false,
         }
         },
  methods:{
     firstImage:function(){
      this.imageProduct = require("@/assets/images/image-product-1.jpg");
      },
      secondImage:function(){
      this.imageProduct = require("@/assets/images/image-product-2.jpg");
      },
      thirdImage:function(){
      this.imageProduct = require("@/assets/images/image-product-3.jpg");
      },
      fourthImage:function(){
      this.imageProduct = require("@/assets/images/image-product-4.jpg");
      },
      add:function(inc){
      this.quantity +=inc;
      },
      subtract:function(dec){
      if(this.quantity >0){
      this.quantity -= dec;
      }
      },
      addToCart:function(){
      this.cartQuantity += this.quantity;
      this.quantity = 0;
      },
      displaySidebar:function(){
       this.showSidebar =! this.showSidebar;
       },
       closeSidebar(){
       this.showSidebar =false;
       },
       cartdetails:function(){
        if(this.cartQuantity > 0){
         this.showFilledAlert =! this.showFilledAlert;
         }
         else{
         this.showEmptyAlert =! this.showEmptyAlert;
         }
         },
         deleteCart:function(){
          this.showFilledAlert = false;
          this.showEmptyAlert =! this.showEmptyAlert;
          this.cartQuantity = 0;
          }
  },
  mounted(){
   if(window.innerWidth <= 768){
    this.showIcon = true;
    }
    }
}
</script>

<style scoped>
@media(max-width:768px){
    *{
    margin:0;
    }
    }
 #main{
    width:1100px;
    border:1px solid grey;
    margin-left:auto;
    margin-right:auto;
    font-family:'Kumbh Sans';
}
@media(max-width:768px){
    #main{
      width:100vw;
      border:none;
      margin:0;
      }
      }
nav{
    display:flex;
    justify-content: space-between;
    margin-left:100px;
    margin-right:100px;
    border-bottom: 1px solid grey;
}
 @media(max-width:768px){
  nav{
     border-bottom:none;
     margin-left:36px;
     margin-right:-120px;
     margin-top:8px;
     }
     }
.options{
      margin-right:16px;
      margin-bottom: 0;
    list-style-type: none;
    display:block;
    cursor:pointer;
  }
  .options:hover{
    border-bottom:2px solid orange;
    color:black;
    }
  @media(max-width:768px){
    .options{
      display:none;
      }
      }
.nav-section{
    display:flex;
    justify-content:center;
    padding:10px 0;
}
.nav-section li {
    margin-right: 16px;
    margin-bottom: 0;
    list-style-type: none;
    color:hsl(219, 9%, 45%);
    
}
.profile-pic:hover{
   border-radius:50%;
   border:2px solid orange;
   cursor:pointer;
   }
#profile-pic{
    width:50px;
    margin-top:-19px;
}
@media(max-width:768px){
  #profile-pic{
      width:35px;
      margin-top:-5px;
      }
      }
#logo{
    width:100px;
    padding-right:20px;
}
 @media(max-width:768px){
   #logo{
      width:225px;
      }
      }
#cart-icn{
    padding-right:20px;
    position:relative;
    cursor:pointer;
}
@media(max-width:768px){
  #cart-icn{
      width:30px;
      }
      }
.badge {
  background-color: #ff5733;
  color: #fff; 
  border-radius: 50%; 
  padding: 1px 1px; 
  position: absolute;
  top:  24px;
  right:323px;
  font-size: 12px; 
}
@media(max-width:768px) {
     .badge{
       right:-43px;
       top:16px;
       }
       }
.orders{
    padding-top:48px;
    padding-left:120px;
    display: flex;
    justify-content: space-between;
    gap:100px;
}
@media(max-width:768px){
    .orders{
      padding-top:12px;
      padding-left:2px;
      flex-direction:column;
      gap:0;
      }
      } 
#img-product{
    width:370px;
    padding-bottom:14px;
    border-top-right-radius:4px;
    border-top-left-radius:4px;
    border-bottom-left-radius:16px;
    border-bottom-right-radius:16px;
}
@media(max-width:768px){
   #img-product{
       width:550px;
       margin-left:-1rem;
       padding-bottom:0;
       }
       }
.img-product{
    width:80px;
    border-radius:6px;
}
.img-product:hover{
   opacity:0.7;
    }
@media(max-width:768px){
   .img-product{
     display:none;
     }
     }
.image-products{
    display:flex;
    gap:16px;
    padding-bottom:4rem;
    border-radius:4px;
}
@media(max-width:768px){
     .image-products{
        padding-bottom:0;
        gap:0;
        }
        }
.orders-details{
    padding-top:4rem;
    padding-right:6rem;
}
@media(max-width:768px){
   .orders-details{
      padding-top:16px;
      padding-left:12px;
      padding-right:0;
      }
      }
h1{
    font-size:16px;
    color:hsl(26, 100%, 55%);
}
@media(max-width:768px){
   h1{
       font-size:18px;
       color:orange;
       }
       }
h2{
    font-size:36px;
}
@media(max-width:768px){
    h2{
      padding-top:10px;
      font-size:42px;
      }
      }
      p{
       color:hsl(219, 9%, 45%);
       }
@media(max-width:768px){
  p{
     padding-top:10px;
     font-size:24px;
     width:130%;
     padding-right:0;
     color:hsl(219, 9%, 45%);
     }
     } 
@media(max-width:768px){
    h3{
      padding-top:24px;
      font-size:24px;
      }
      }
span{
    padding-left: 12px;
    color:hsl(26, 100%, 55%);
    padding-right: 12px;
    font-size:16px;
}
@media(max-width:768px){
   span{
    font-size:20px;
    margin-left:24px;
    }
    }
#normal-price{
    transform: translateY(-10px);
    font-size:14px;
    color:hsl(219, 9%, 45%);
}
@media(max-width:768px){
  #normal-price{
      padding-left:28rem;
      transform:translateY(-38px);
      font-size:18px;
      }
      }
.cart-section{
    display:flex;
    gap:30px;
    margin-top:-6px;
}
@media(max-width:768px){
   .cart-section{
      flex-direction:column;
      gap:30px;
      justify-content:space-between;
      }
      }
.add-cart{
    display:flex;
    align-items: center;
    gap:20px;
    border:1px solid grey;
    border-radius: 4px;
    height:20px;
    padding-left:8px;
    padding-right:8px;
    padding-top:2px;
    padding-bottom:2px;
}
@media(max-width:768px){
  .add-cart{
    gap:215px;
    padding-left:10px;
    padding-right:10px;
    margin-right:auto;
    padding-top:12px;
    padding-bottom:12px;
    }
    }
#cart-icon{
    width:16px;
    color:#fff;
}
@media(max-width:768px){
 #cart-icon{
   width:24px;
   }
   }
button{
    border-radius: 6px;
    border-color:hsl(26, 100%, 55%);
    padding-left:36px;
    padding-right:36px;
    padding-top: 6px;
    padding-bottom: 6px;
    margin-top:-6px;
    color:#fff;
    background:hsl(26, 100%, 55%);
    cursor:pointer;
}
button:hover{
    opacity:0.7;
    }
@media(max-width:768px){
 button{
   padding-top:14px;
   padding-bottom:14px;
   background:orange;
   width:510px;
   color:#fff;
   font-size:24px;
   }
}
@media(max-width:768px){
     strong{
        font-size:22px;
        }
    }
    #icon-minus{
      cursor:pointer;
      }
     #icon-minus:hover{
       opacity:0.7;
       }

      #icon-plus{
        cursor:pointer;
        }
        #icon-plus:hover{
         opacity:0.7;
         }
@media(max-width:768px){
   #icon-minus{
      width:20px;
      }
    }
@media(max-width:768px){
   #icon-plus{
     width:20px;
     }
    }
</style>
