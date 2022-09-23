<template>
  <view class="warp">
    <text
      :class="{ red: judgeHigh(item) }"
      v-for="(item, index) in highlightList"
      :key="index"
      >{{ item }}</text
    ></view
  >
</template>

<script>
export default {
  name: "highlight",
  props: {
    strText: {
      type: String,
      default: () => "",
    },
  },
  watch: {
    strText(val) {
      // 根据span标签切割
      this.splitTextByTag();
      // 根据span标签获取高亮的关键字
      this.getKeyWordByTag();
    },
  },
  computed: {
    // 高亮判断
    judgeHigh() {
      return function (item) {
        if (this.keyArr.length > 0) {
          if (this.keyArr.includes(item)) {
            return true;
          } else {
            return false;
          }
        } else {
          return false;
        }
      };
    },
  },
  data() {
    return {
      highlightList: [], //处理后的数据
      keyArr: [], // 高亮关键字
    };
  },
  created() {
    // 根据span标签切割
    this.splitTextByTag();
    // 根据span标签获取高亮的关键字
    this.getKeyWordByTag();
  },
  /**
   * 组件的方法列表
   */
  methods: {
    getKeyWordByTag() {
      let str = this.strText;
      let domReg = /(?:(<span[^>]*?>)).*?(?:(<\/span>))/g;
      let arr = str.match(domReg) || [];
      this.keyArr = arr.map((e) => {
        return e.match(/<span style=color:red>([\s\S]*?)<\/span>/)[1];
      });
    },
    splitTextByTag() {
      let str = this.strText;
      const reg = /<span[^>]*?>|<\/span>/g;
      this.highlightList = str.split(reg) || [];
    },
  },
};
</script>
<style lang="scss" scoped>
.warp {
  display: inline;
  width: 100%;
}
.red {
  color: red;
}
</style>
