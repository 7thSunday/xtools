<template>
  <div>
    <tool-header :disc="disc"></tool-header>
    <div class="op-area">
      <el-row>
        <el-col :span="2"><el-tag type="info" >ASCII</el-tag></el-col>
        <el-col :span="22">
          <el-input
            type="textarea"
            :rows="3"
            placeholder="ASCII"
            v-model="asc2"
            @input="handleASC2Change"
          ></el-input>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="2"><el-tag type="info" >二进制</el-tag></el-col>
        <el-col :span="22">
          <el-input
            type="textarea"
            :rows="3"
            placeholder="二进制"
            v-model="bin"
            @input="handleBinChange"
          ></el-input>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="2"><el-tag type="info" >十进制</el-tag></el-col>
        <el-col :span="22">
          <el-input
            type="textarea"
            :rows="3"
            placeholder="十进制"
            v-model="dec"
            @input="handleDecChange"
          ></el-input>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="2"><el-tag type="info" >十六进制</el-tag></el-col>
        <el-col :span="22">
          <el-input
            type="textarea"
            :rows="3"
            placeholder="十六进制"
            v-model="hex"
            @input="handleHexChange"
          ></el-input>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import toolHeader from "./toolHeader.vue";
import BigNumber from "bignumber.js"
export default {
  components: { toolHeader },
  computed: {
    list() {
      return this.$store.state.Counter.list;
    },
  },
  data() {
    return {
      disc:"",
      asc2:"",
      bin:"",
      dec:"",
      hex:""
    };
  },
  methods: {
    pad (pad, str, padLeft) {
      if (typeof str === 'undefined') 
        return pad;
      if (padLeft) {
        return (pad + str).slice(-pad.length);
      } else {
        return (str + pad).substring(0, pad.length);
      }
    },
    handleASC2Change() {
      let textarr = this.asc2.split('');
      let hex = "";
      let dec = "";
      let bin = "";
      textarr.forEach((x)=>{
        hex = hex + this.pad('00',x.charCodeAt().toString(16),true) + " ";
        dec = dec + x.charCodeAt() + " ";
        bin = bin + this.pad('00000000',x.charCodeAt().toString(2),true) + " ";
      });
      this.bin = bin.replace(/^\s|\s$/g,"")
      this.dec = dec.replace(/^\s|\s$/g,"")
      this.hex = hex.replace(/^\s|\s$/g,"");
    },
    handleBinChange() {
      let bin = this.bin.replace(/^\s|\s$/g,"");
      let binarr = bin.split(' ');
      let text = "";
      let hex = "";
      let dec = "";
      binarr.forEach((x)=>{
        hex = hex + this.pad('00',new BigNumber(x, 2).toString(16),true) + " ";
        dec = dec + new BigNumber(x, 2) + " ";
        text = text + String.fromCharCode(new BigNumber(x, 2));
      });
      this.asc2 = text;
      this.dec = dec;
      this.hex = hex.replace(/^\s|\s$/g,"");
    },
    handleDecChange() {
      let dec = this.dec.replace(/^\s|\s$/g,"");
      let decarr = dec.split(' ');
      let text = "";
      let hex = "";
      let bin = "";
      decarr.forEach((x)=>{
        bin = bin + this.pad('00000000',new BigNumber(x, 10).toString(2),true) + " ";
        hex = hex + this.pad('00',new BigNumber(x, 10).toString(16),true) + " ";
        text = text + String.fromCharCode(new BigNumber(x, 10));
      });
      this.asc2 = text;
      this.hex = hex.replace(/^\s|\s$/g,"");
      this.bin = bin.replace(/^\s|\s$/g,"");
    },
    handleHexChange() {
      let hexarr = this.hex.split(" ");
      let bin = "";
      let dec = "";
      let text = "";
      hexarr.forEach((x)=>{
        bin = bin + this.pad('00000000',new BigNumber(x, 16).toString(2),true) + " ";
        dec = dec + new BigNumber(x, 16).toString(10) + " ";
        text = text + String.fromCharCode(new BigNumber(x, 16));
      });
      this.asc2 = text;
      this.dec = dec.replace(/^\s|\s$/g,"");
      this.bin = bin.replace(/^\s|\s$/g,"");
    }
  },
  created() {
    for (let item of this.list) {
      if (item.id == "jinzhi") {
        this.disc = item.disc;
        break;
      }
    }
  },
};
</script>

<style lang="scss">
</style>