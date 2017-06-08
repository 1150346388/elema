<template>
  <div>
   <side-bar :sides="list" :defaultid='1'></side-bar>
  </div>
</template>

<script type="text/ecmascript-6">
import sideBar from '../header/sideBar.vue';

export default {
	data() {
		return {
			list:
        [{'id': 1, 'add': '上海', 'pid': ' '}, {'id': 2, 'add': '江苏', 'pid': ' '}, {'id': 11, 'add': '浦东', 'pid': 1}, {'id': 12, 'add': '徐汇', 'pid': 1}, {'id': 13, 'add': '静安', 'pid': 1}, {'id': 111, 'add': '北蔡', 'pid': 11}, {'id': 112, 'add': '南汇', 'pid': 11}, {'id': 121, 'add': '九亭', 'pid': 12}, {'id': 21, 'add': '南京', 'pid': 2}, {'id': 22, 'add': '盐城', 'pid': 2}, {'id': 211, 'add': '江宁', 'pid': 21}, {'id': 221, 'add': '东台', 'pid': 22}]
		};
	},
  components: {
      sideBar
  },
  methods: {
  },
	created() {
  }
};
</script>