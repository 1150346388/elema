<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <a v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
import header from 'components/header/header.vue';

const ERROR_NO = 0;
export default {
 data() {
   return {
     seller: {}
   };
 },
 created() {
   this.$http.get('/api/seller').then((res) => {
   if (res.body.errno === ERROR_NO) {
       this.seller = res.body.data;
   }
      console.log(this.seller);
   });
 },
 components: {
    'v-header': header
 }
 };
</script>
<style lang="stylus" rel="stylesheet/stylus">
  .tab-item
    display:inline-block
    width:32.3%
    text-align:center
    a
      display:block
</style>