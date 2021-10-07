<template>
  <div>
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
      <el-row :gutter="10">
        <el-col :span="6">
          <el-input
            v-model="paramA"
            placeholder="(1,3,5,7,9,11,15,17,19,21,23)"
          ></el-input>

        </el-col>
        <el-col :span="6">
          <el-input
            v-model="paramB"
            placeholder="(0-25)"
          ></el-input>
        </el-col>
        <el-col
          :span="4"
          class="btns"
          :offset="8"
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
export default {
  components: { toolHeader },
  computed: {
    list() {
      return this.$store.state.Counter.list;
    },
  },
  data() {
    return {
      result: "",
      paramA: "",
      paramB: "",
      textarea: "",
    };
  },
  methods: {
    handleClickEncode() {},
    handleClickDecode() {
      let aGroup = this.paramA
        ? [this.paramA]
        : [3, 5, 7, 9, 11, 15, 17, 19, 21, 23];
      let res = [];
      let charGroup = this.getPosGroup();
      for (let i = 0; i < 26; i++) {
        let temp = [];
        for (let j of aGroup) {
          let niA = this.getNI(j);
          for (let c of charGroup) {
            if (c.type == "o") {
              temp.push(c.data);
            } else {
              let comp = ((c.data - i) * niA) % 26;
              c.type == "u"
                ? temp.push(String.fromCharCode(comp + 65))
                : temp.push(String.fromCharCode(comp + 97));
            }
          }
          res.push(temp.join(""));
          temp = [];
        }
      }
      this.result = res.join("\n");
    },
    getPosGroup() {
      let arr = this.textarea.split("");
      for (let i in arr) {
        let obj = {
          data: arr[i],
          type: "o",
        };
        if (arr[i].charCodeAt() >= 65 && arr[i].charCodeAt() <= 90) {
          obj.data = arr[i].charCodeAt() - 65;
          obj.type = "u";
        } else if (arr[i].charCodeAt() >= 97 && arr[i].charCodeAt() <= 122) {
          obj.data = arr[i].charCodeAt() - 97;
          obj.type = "l";
        }
        arr[i] = obj;
      }
      return arr;
    },
    getNI(x) {
      let i = 1;
      while ((x * i) % 26 != 1) i++;
      return i;
    },
  },
  created() {
    for (let item of this.list) {
      if (item.id == "affineCipher") {
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
</style>