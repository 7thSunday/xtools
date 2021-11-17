<template>
  <div class="">
    <tool-header :disc="disc"></tool-header>
    <div class="op-area">
      <el-row>
        <el-input
          type="textarea"
          clearable=""
          :rows="3"
          placeholder="请输入内容"
          v-model="textarea"
        >
        </el-input>
      </el-row>
      <el-row>
        <el-col
          :span="4"
          :offset="15"
          class="btns"
        >
          <el-button
            type="primary"
            @click="handleClickEncode"
          >编码</el-button>
          <el-button
            type="primary"
            @click="handleClickDecode"
          >解码</el-button>
        </el-col>
      </el-row>
      <el-row v-show="result.length">
        <el-input
          type="textarea"
          readonly=""
          :rows="3"
          v-model="result"
        >
        </el-input>
      </el-row>
    </div>
  </div>
</template>

<script>
import toolHeader from "./toolHeader.vue";
import { decode, encode } from 'xmorse';
// const Base32 = require("base-32").default;
export default {
  components: { toolHeader },
  computed: {
    list() {
      return this.$store.state.Counter.list;
    },
  },
  data() {
    return {
      disc: "",
      textarea: "",
      typeSelector: "64",
      result: "",
      option: {
        space: ' ',
        long: '-',
        short: '.'
      }
    };
  },
  methods: {
    handleClickEncode() {
      this.result = encode(this.textarea, this.option);
    },
    handleClickDecode() {
      this.result = decode(this.textarea, this.option);
    },
  },
  created() {
    for (let item of this.list) {
      if (item.id == "morse") {
        this.disc = item.disc;
        break;
      }
    }
  },
};
</script>

<style lang="scss">
.btns {
  display: flex;
  justify-content: space-between;
}
.result {
  border: 1px dashed #555;
}
</style>