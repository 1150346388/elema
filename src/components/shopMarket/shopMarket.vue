<template>
  <div class="market">
    <ul v-if="foods">
      <li class="food_item" v-for="food in foods" track-by="$index">
        <div v-if="food.count"><span>{{food.name}}</span><span @click="minus(food)">-</span>{{food.count}}<span @click="pluss(food)">+</span></div>
      </li>
    </ul>
    <div class="total">
      <span>{{total | toCash}}</span><button v-if="total < minPrice" :disabled="total < minPrice">¥{{total===0 ? seller.minPrice : `还差`+(seller.minPrice-total | toCash)}}起送</button><button v-else>确认</button>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
const ERROR_NO = 0;
export default {
  props: {
    foods: {
      type: Array
    },
    total: {
      type: Number
    }
  },
data() {
   return {
     seller: {},
     minPrice: 0
   };
 },
 created() {
   this.$http.get('/api/seller').then((res) => {
   if (res.body.errno === ERROR_NO) {
       this.seller = res.body.data;
   }
      this.minPrice = this.seller.minPrice;
      console.log(this.total < this.minPrice);
   });
 },
  updated() {
    console.log(this.foods);
  },
  methods: {
    pluss(food) {
      food.count++;
      if (food.count === 1) {
      this.foods.push(food);
      }
      this.total = 0;
    this.foods.forEach((f) => {
     this.total += (f.count * f.price);
    });
    },
    minus(food) {
      food.count === 0 ? food.count = 0 : food.count--;
      if (food.count === 0) {
        this.$lodash.remove(this.foods, function(f) {
         return f === food;
        });
      }
      this.total = 0;
    this.foods.forEach((f) => {
     this.total += (f.count * f.price);
    });
    }
  },
  filters: {
    toCash(c) {
      return '¥' + c;
    }
  }
};
</script>
<style lang="stylus" rel="stylesheet/stylus">
.market
  position:absolute
  bottom:0
  width:100%
  ul
    display:inline-block
    width:60%
  .total
    display:inline-block
    width:38% 
    button
      border:1px solid #000
</style>