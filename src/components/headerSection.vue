<template>
  <div id="main">
    <header>
    <nav>
            <ul class="nav-section">
                <sidebar :showSidebar = "showSidebar" :closeSidebar = "closeSidebar"></sidebar>
                <!-- <icon-component :showIcon="showIcon" :displaySidebar="displaySidebar"></icon-component> -->
                  <img src="@/assets/images/icon-menu.svg" alt=""  v-on:click="displaySidebar" class="hamburger-icon">
                <li><img src="@/assets/images/logo.svg" alt="logo" id="logo"></li>
                <li class="options" v-for="option in options" v-bind:key="option.id">{{option.name}}</li>
            </ul>
            <ul class="nav-section">
                <filled-cart v-if="showFilledAlert" :priceProp = "price" :cartQuantityProp = "cartQuantity" :deleteCart = "deleteCart"></filled-cart>
                 <empty-cart v-if="showEmptyAlert"></empty-cart>
                 <div class="notification-icon">
                <li><img src="@/assets/images/icon-cart.svg" alt="cart-icon" id="cart-icn" v-on:click="cartdetails" >
                <span class="badge" v-if="cartQuantity > 0">{{cartQuantity}}</span> </li>
                </div>
                <li><img src="@/assets/images/image-avatar.png" alt="profile-pic" id="profile-pic" class="profile-pic"></li>
            </ul>
    </nav>
   </header>
     <section class="orders">
    <div>
        <light-box :images="images" ref="lightbox" v-if="lightboxOpen"/>
        <img :src="imageProduct" alt="image-product1" id="img-product" @click="openLightbox()">
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
import alertFilledCart from '@/components/alertFilledCart.vue';
import alertEmptyCart from '@/components/alertEmptyCart.vue';
import LightBox from '@/components/LightBox.vue';
export default {
  components: {
      'sidebar':sideBar,
      'filled-cart':alertFilledCart,
      'empty-cart':alertEmptyCart,
      LightBox,
  },
  data(){
  return{
  
  imageProduct:require("@/assets/images/image-product-1.jpg"),
   options:[
              {id:1,name:'Collections'},
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
 images:[require('@/assets/images/image-product-1.jpg'),
      require('@/assets/images/image-product-2.jpg'), 
      require('@/assets/images/image-product-3.jpg'),
      require('@/assets/images/image-product-4.jpg')
],
     lightboxOpen:false
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
          },
          openLightbox(){
            this.lightboxOpen = true;
            this.$refs.lightbox.show();
          }
  },
  
}
</script>

<style scoped>
*{
  margin:0;
  padding:0;
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
      width:100%;
      border:none;
      margin:0;
      }
      }
nav{
    display:flex;
    justify-content: space-between;
    padding-top:24px;
    padding-left:100px;
    padding-right:100px;
    border-bottom: 1px solid grey;
}
 @media(max-width:768px){
  nav{
     border-bottom:none;
     padding-left:0;
     padding-right:0;
     padding-top:8px;
     justify-content:none;

      
     }
     }
.options{
      padding-right:16px;
      padding-bottom:-9.5px;
    list-style-type: none;
    display:block;
    cursor:pointer;
  }
.options:hover {
   border-bottom:2px solid orange;
   }
  @media(max-width:768px){
    .options{
      display:none;
      }
      }
ul{
    display:flex;
    justify-content:center;
    padding:10px 0;
}
@media(max-width:768px){
    ul{
        padding:3px 0;
    }
}
ul li {
    padding-right: 16px;
    padding-bottom: 0;
    list-style-type: none;
    color:hsl(219, 9%, 45%);
    
}
@media (max-width:768px){
    ul li{
        padding-right:0;
    }
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
      padding-right:1rem;
      }
      }
#logo{
    width:100px;
    padding-right:20px;
}
 @media(max-width:768px){
   #logo{
      width:170px;
      padding-left:15px;
      padding-right:0;
      }
      }
.notification-icon{
     position:relative;
     display:inline-block;
     }
#cart-icn{
    padding-right:20px;
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
  top:-8px;
  right:35px;
  font-size: 12px; 
}
@media(max-width:768px) {
     .badge{
       right:20px;
       top:-8px;
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
       width:100%;
       padding-left:0;
       padding-bottom:0;
       border-radius: 0;
       padding-right:-2rem;
       
       }
       }
.img-product{
    width:80px;
    border-radius:6px;
}
.img-product:hover{
   opacity:0.7;
    }
.img-product:active{
    border:2px solid orange;
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
    padding-top:28px;
}
@media(max-width:768px){
    h2{
      padding-top:20px;
      font-size:36px;
      padding-right:0;
      }
      }
      p{
       color:hsl(219, 9%, 45%);
       padding-top:12px;
       line-height:1.5;
       }
@media(max-width:768px){
  p{
     padding-top:20px;
     font-size:16px;
     padding-right:0;
     color:hsl(219, 9%, 45%);
     }
     } 
     h3{
        padding-top:12px;
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
    padding-left:12px;
    }
    }
#normal-price{
    font-size:14px;
    color:hsl(219, 9%, 45%);
}
@media(max-width:768px){
  #normal-price{
      padding-left:16rem;
      transform:translateY(-50px);
      font-size:20px;
      }
      }
.cart-section{
    display:flex;
    gap:30px;
    padding-top:10px;
}
@media(max-width:768px){
   .cart-section{
      flex-direction:column;
      gap:30px;
      align-items:center;
      margin:0;
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
    gap:140px;
    padding-top:12px;
    padding-left:-1.4rem;
    padding-bottom:12px;
    margin-right:12px;
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
    border:none;
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
   
   width:350px;
   padding-top:14px;
   padding-bottom:14px;
   background:orange;
   color:#fff;
   font-size:24px;
   padding-left:12px;
   margin-right:12px;
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
    .hamburger-icon{
        display:none;
        width:24px;
  padding-right:0;
  padding-top:5px;
    }
@media(max-width:768px){
    .hamburger-icon{
        display: block;
    }
}
</style>
