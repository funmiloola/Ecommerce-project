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
           <img src="@/assets/images/image-product-1-thumbnail.jpg" alt="" class="img-product">
            <img src="@/assets/images/image-product-2-thumbnail.jpg" alt="" class="img-product">
            <img src="@/assets/images/image-product-3-thumbnail.jpg" alt="" class="img-product">
            <img src="@/assets/images/image-product-4-thumbnail.jpg" alt="" class="img-product">
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
    show(index){
        this.visible = true;
        this.currentIndex = index;
    },
    hide(){
        this.visible = false;
        this.currentIndex = 0;
    },
    hasNext(){
        return this.currentIndex + 1 < this.images.length;
    },
    hasPrev(){
        return this.currentIndex - 1 >= 0; 
    },
    next(){
        if(this.hasNext()){
            this.currentIndex += 1;
        }
    },
    prev(){
        if(this.hasPrev()){
            this.currentIndex -= 1;
        }
    }
  }
}
</script>
<style scoped>
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
    width:375px;
    position:relative;
}
#icn-previous{
    position:absolute;
    top:13.5rem;
    left:17rem;
    border-radius:50%;
    background: #fff;
    width:10px;
    padding-top:0.5rem;
    padding-left:0.7rem;
    padding-right: 0.7rem;
    padding-bottom:0.5rem;
}
#icon-next{
    position:absolute;
    top:13.5rem;
    right:39.7rem;
    border-radius:50%;
    background: #fff;
    width:10px;
    padding-top:0.5rem;
    padding-left:0.7rem;
    padding-right: 0.7rem;
    padding-bottom:0.5rem;
}
/* #close-icon{
   float:right;
   padding-right:20.5rem;
   padding-bottom:1rem;
} */
.thumbnails-section{
     display:flex;
     gap:10px;
     padding-top:8px;
}
.img-product{
    width:90px;
    border-radius:8px;
}
</style>