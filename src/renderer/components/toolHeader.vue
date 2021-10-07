<template>
  <div class="tool-header">
    <div class="disc">
      <span>----</span>
      <span>{{disc}}</span>
      <span>----</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    disc: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss">
.tool-header {
  font-family: "Microsoft YaHei", Helvetica, sans-serif;
  font-size: 12px;
  color: #777;
  margin-bottom: 16px;
}
</style>