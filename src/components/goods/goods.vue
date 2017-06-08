<template>
  <div class="goods">
    <div class="menu_wapper">
    	<ul>
    		<li v-for="item in goods" class="item_good"><span>{{item.name}}</span></li>
    	</ul>
    </div>
    <div class="foods_wapper">
       <div v-for="item in goods">
       <div class="title">{{item.name}}</div>
    	<ul>
    		<li v-for="food in item.foods" class="food_item">
    			<img :src="food.image">
    			<div class="info">
    				<p class="title">{{food.name}}</p>
    				<p>{{food.description}}</p>
    				<p>月销售{{food.sellCount}}份 好评率{{food.rating}}%</p>
            <span>¥{{food.price}}</span><span class="minus" @click="minus(food)">-</span>{{food.count}}<span class="pluss" @click="pluss(food)">+</span>
    			</div>

    		</li>
    	</ul>       	
       </div>
    </div>
  </div>
  <market :foods="foods" :total="total" ></market>
</template>

<script type="text/ecmascript-6">
import market from '../shopMarket/shopMarket.vue';
import lodash from 'lodash';

export default {
	data() {
		return {
			goods: [],
			foods: [],
      total: 0
		};
	},
  components: {
      market
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
        lodash.remove(this.foods, function(f) {
         return f === food;
        });
      }
      this.total = 0;
    this.foods.forEach((f) => {
     this.total += (f.count * f.price);
    });
    }
  },
	created() {
		this.$http.get('/api/goods').then((res) => {
              res.body.data.forEach((good) => {
                good.foods.forEach((food) => {
                  food.count = 0;
                 });
              });
              this.goods = res.body.data;
              console.log(this.goods[0]);
		});
	}
};
</script>
<style lang="stylus" rel="stylesheet/stylus">
.goods
  position:absolute
  top:174px
  bottom:46px
  width:100%
  display:flex
  overflow:hidden
  .menu_wapper
    flex:0 0 80px
    width:80px
    background:#f3f5f7
  .foods_wapper
    flex:1
    overflow:auto
    .food_item
      img
        width:60px
      .info 
        display:inline-block
        .minus
          font-size:14px
</style>