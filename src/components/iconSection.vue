<template>
  <div class="icon">
    <img src="@/assets/images/icon-menu.svg" alt="" v-if="showIcon" v-on:click="displaySidebar">
  </div>
</template>
<script>
export default {
  props: {
    showIcon: Boolean,
    displaySidebar: Function
  }
}
</script>
<style scoped>
 img{
  width:24px;
  padding-right:20px;
  padding-top:8px;
  }
</style>