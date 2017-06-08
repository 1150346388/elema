<template>
  <div class="side">
  <select v-for="parts in cities" track-by="$index" @change="changeHadler($index,$event)">
    <template v-for="city in parts">
      <option :value="city.id"  v-if="city.show"><span>{{city.add}}</span></option> 
    </template>

  </select>
  </div>
</template>

<script type="text/ecmascript-6">
import lodash from 'lodash';

export default {
	props: {
	sides: {
	type: Array
	},
  defaultid: {
    type: Number
  }
	},
	data() {
		return {
           cities: [],
           citys: [],
           ids: [],
           pids: []
		};
	},
  created() {
    let p = [];
    lodash.forEach(this.sides, (n, key) => {
        let tp = Object.assign({}, n, {'show': true});
        this.ids.push(n.id);
        this.pids.push(n.pid);
        if (n.pid === ' ') {
             p.push(tp);
        }
    });
    this.cities.push(p);
    this.citys = this.cities[0];
    this.arrayHandlar(this.cities[0]);
    console.log(this.cities);
  },
  methods: {
    arrayHandlar(a) {
    if (this.$lodash.flattenDeep(this.cities).length !== this.sides.length) {
    let ps = [];
    for (var i = 0; i < a.length; i++) {
       for (var j = 0; j < this.sides.length; j++) {
         if (a[i].id === this.sides[j].pid) {
          let np = Object.assign({}, this.sides[j], {'show': a[0].id === this.sides[j].pid});
          ps.push(np);
         }
       }
     }
    this.cities.push(ps);
    this.arrayHandlar(ps);
  } else {
    this.terminal = this.cities.length - 1;
    return this.cities;
}
    },
    changeHadler(index, e) {
      let i = index + 1;
      lodash.forEach(this.cities[i], (n, key) => {
        if (n.pid.toString() !== e.target.value.toString()) {
             n.show = false;
        } else {
             n.show = true;
        }
      });
      if (lodash.includes(lodash.difference(this.ids, this.pids), e.target.value.toString())) {
           console.log(e.target.value);
      }
      this.cities = Object.assign({}, this.cities);
      console.log(lodash.difference(this.ids, this.pids)[0] === e.target.value.toString());
      console.log(lodash.difference(this.ids, this.pids));
    },
    diguiHadler(index, ids) {

    }
  }
};
</script>
<style lang="stylus" rel="stylesheet/stylus">
</style>