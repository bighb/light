<template>
  <view class="warp">
    <text
      :class="{ red: judgeHigh(item) }"
      v-for="(item, index) in sliceArr"
      :key="index"
      >{{ item }}</text
    ></view
  >
</template>

<script>
const getInf = (str, key) =>
  str
    .replace(new RegExp(`${key}`, "gi"), (txt) => {
      return `%%${txt}%%`;
    })
    .split("%%");
export default {
  name: "highlight-slice",
  props: {
    strText: {
      type: String,
      default: () => "",
    },
    keyWord: {
      type: String,
      default: () => "",
    },
  },
  computed: {
    sliceArr() {
      if (this.strText) {
        return getInf(this.strText, this.keyWord);
      } else {
        return [];
      }
    },
    // 高亮判断
    judgeHigh() {
      return function (name) {
        if (name) {
          let lowName = name.toLowerCase();
          let lowKeyword = this.keyWord.toLowerCase();
          if (lowName === lowKeyword) {
            return "highlight";
          } else {
            return "";
          }
        } else {
          return "";
        }
      };
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
