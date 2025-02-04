<template>
  <div v-if="visible" class="lightbox">
    <div class="lightbox-content" >
    <img src="@/assets/images/icon-close.svg" alt="close-icon" id="close-icon" @click="hide"/>
    <div class="lightbox-images">
    <img :src="images[currentIndex]" alt="lightbox-image" id="lightbox-images">
    </div>
    <div class="lightbox-control">
    <img src="@/assets/images/icon-previous.svg" alt="icon-previous" id="icn-previous" @click="prev">
    <img src="@/assets/images/icon-next.svg" alt="icon-next" id="icon-next" @click="next">
    </div>
    <div class="thumbnails-section">
           <img src="@/assets/images/image-product-1-thumbnail.jpg" alt="" class="img-product" @click="selectImage(0)" :class="{'selected': isSelected(0)}">
            <img src="@/assets/images/image-product-2-thumbnail.jpg" alt="" class="img-product" @click="selectImage(1)" :class="{'selected': isSelected(1)}">
            <img src="@/assets/images/image-product-3-thumbnail.jpg" alt="" class="img-product" @click="selectImage(2)" :class="{'selected': isSelected(2)}">
            <img src="@/assets/images/image-product-4-thumbnail.jpg" alt="" class="img-product" @click="selectImage(3)" :class="{'selected':isSelected(3) }">
    </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    images:{
        type:Array,
        required:true,
    }
  },
  data(){
    return{
        visible:false, 
        currentIndex:0,
    }
  },
  methods:{
    show(){
        this.visible = true;
    },
    hide(){
        this.visible = false;
        this.currentIndex = 0;
    },
    next(){
        if(this.currentIndex + 1 < this.images.length){
            this.currentIndex += 1;
        }
    },
    prev(){
        if(this.currentIndex - 1 >= 0){
            this.currentIndex -= 1;
        }
    },
    selectImage(index){
        this.visible = true;
        this.currentIndex = index;
    }
  },
  computed:{
    isSelected(){
        return (index) => this.currentIndex == index;
    }
  }
}
</script>
<style scoped>
@media(max-width:768px){
.lightbox{
    visibility: hidden;
}
}
 .lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}
#lightbox-images{
    width:380px;
    position:relative;
    margin-left:auto;
    margin-right:auto;
}
#icn-previous{
    position:absolute;
    top:17rem;
    left:29rem;
    border-radius:50%;
    background: #fff;
    width:10px;
    padding-top:0.5rem;
    padding-left:0.7rem;
    padding-right: 0.7rem;
    padding-bottom:0.5rem;
    cursor: pointer;
}
#icon-next{
    position:absolute;
    top:17rem;
    right:30rem;
    border-radius:50%;
    background: #fff;
    width:10px;
    padding-top:0.5rem;
    padding-left:0.7rem;
    padding-right: 0.7rem;
    padding-bottom:0.5rem;
    cursor: pointer;
}
#close-icon{
   float:right;
   padding-right:1rem;
   padding-bottom:1rem;
   cursor:pointer;
   color:white;
}
#close-icon:hover{
    color:orange;
}
.thumbnails-section{
     display:flex;
     gap:10px;
     padding-top:12px;
}
.img-product{
    width:90px;
    border-radius:8px;
}
.img-product:hover{
     opacity:0.7;
}
.selected{
    border:2px solid orange;
}
</style>