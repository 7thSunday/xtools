<template>
  <div class="base64">
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
        <el-col :span="5">
          <el-select
            v-model="typeSelector"
            placeholder="请选择"
          >
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-col>
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
import { Base64, encodeURL } from "js-base64";
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
      options: [
        {
          value: "64",
          label: "base64",
        },
        // {
        //   value: "32",
        //   label: "base32",
        // },
      ],
    };
  },
  methods: {
    handleClickEncode() {
      switch (this.typeSelector) {
        case "64":
          this.result = Base64.encode(this.textarea);
          break;
        // case "32":
        //   this.result = Base32.encode(this.textarea);
        //   break;
      }
    },
    handleClickDecode() {
      switch (this.typeSelector) {
        case "64":
          this.result = Base64.decode(this.textarea);
          break;
        // case "32":
        //   this.result = Base32.decode(this.textarea);
        //   break;
      }
    },
  },
  created() {
    for (let item of this.list) {
      if (item.id == "base64") {
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