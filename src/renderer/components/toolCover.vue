<template>
  <div class="tool-cover">
    <div class="title">{{title}}</div>
    <div class="disc">{{disc}}</div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "title",
    },
    disc: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss">
.tool-cover {
  border: 1px solid #e5e5e5;
  font-family: "Microsoft YaHei", Helvetica, sans-serif;
  padding: 5px 10px;
  border-radius: 10px;
  .title {
    border-bottom: 1px solid #e5e5e5;
    padding-bottom: 5px;
    color: #333;
  }
  .disc {
    padding-top: 5px;
    font-size: 12px;
    color: #555;
    height: 34px;
  }
}
</style>