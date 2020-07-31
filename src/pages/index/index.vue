<template>
  <div id="app">
    <vueEditor ref="editor"></vueEditor>
    <span @click="getHtml">获取值</span>
  </div>
</template>

<script>
// import vueEditor from "../../components/editor.vue";

import vueEditor from "vue-editor-phone/src/components/editor.vue";
console.log(vueEditor)

export default {
  components: {
    vueEditor: vueEditor
  },
  data() {
    return {};
  },
  mounted() {
    // 上传图片服务器参数
    this.$refs.editor.uploadImgServer =
      "http://192.168.15.215:31302/platformplugin/uploadFile.do";
    // 设置值
    this.$refs.editor.setHtml(
      '<div>您好，请编辑</div><div style="width: 100%;"><img src="https://si.geilicdn.com/pcitem1276928634-691b000001734b284ff70a20b7b9_720_550.jpg.webp?w=160&amp;h=160" style="max-width:100%;"></div>'
    );
  },
  methods: {
    // 获取值
    getHtml() {
      console.log(this.$refs.editor.getHtml());
    }
  }
};
</script>


<style scoped>
</style>
