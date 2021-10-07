<template>
  <div class="container">
    <el-row
      :gutter="10"
      v-for="(row, index) in rows"
      :key="index"
    >
      <el-col
        :span="6"
        v-for="(col, j) in row"
        :key="j"
      >
        <tools-cover
          :title="col.name"
          :disc="col.disc"
          @click.native="handleClickCover(col)"
        ></tools-cover>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import toolsCover from "../components/toolCover.vue";
export default {
  components: { toolsCover },
  data() {
    return {
      rows: [],
    };
  },
  computed: {
    list() {
      return this.$store.state.Counter.list;
    },
  },
  mounted() {
    let temp = [];
    for (let i = 1; i <= this.list.length; i++) {
      temp.push(this.list[i - 1]);
      if (i % 4 == 0) {
        this.rows.push(temp);
        temp = [];
      }
    }
    if (this.list.length < 4) {
      this.rows.push(temp);
    }
  },
  methods: {
    handleClickCover(tabObj) {
      this.$emit("on-click-cover", tabObj);
    },
  },
};
</script>

<style lang="scss">
.el-row {
  margin-bottom: 10px;
  &:last-child {
    margin-bottom: 0;
  }
}
</style>