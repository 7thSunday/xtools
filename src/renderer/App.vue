<template>
  <div id="app">
    <el-tabs v-model="currentTab">
      <el-tab-pane
        key="home"
        label="主页"
        name="home"
      >
        <home @on-click-cover="handleOpen"></home>
      </el-tab-pane>
      <el-tab-pane
        v-for="item in tabsGroup"
        :key="item.id"
        :label="item.name"
        :name="item.id"
      >
        <component :is="item.id"></component>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import home from "./pages/Home.vue";
import base64 from "./components/base64.vue";
import affineCipher from "./components/affineCipher.vue";
export default {
  name: "xtools",
  components: { home, base64, affineCipher },
  data() {
    return {
      tabsGroup: [],
      currentTab: "home",
    };
  },
  methods: {
    handleOpen() {
      let tabObj = arguments[0];
      if (this.checkOpenStatus(tabObj.id)) {
        this.currentTab = tabObj.id;
        return;
      }
      let newTab = {
        name: tabObj.name,
        id: tabObj.id,
      };
      this.tabsGroup.push(newTab);
      this.currentTab = tabObj.id;
    },
    checkOpenStatus(id) {
      for (let tab of this.tabsGroup) {
        if ((tab.id = id)) return true;
      }
      return false;
    },
  },
};
</script>

<style>
/* CSS */
</style>
