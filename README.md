# vue-editor
```
vue-editor-phone 是一个 Vue 的移动端富文本编辑器插件，简洁灵活可扩展
```
## 安装
```
npm install vue-editor-phone
```

### 引用
```
import vueEditor from "vue-editor-phone/src/components/editor.vue";

```

### 局部注册
```
components: {
    vueEditor: vueEditor
}
```

### 标签
```
<vueEditor ref="editor"></vueEditor>
```

### 上传图片服务器参数
```
this.$refs.editor.uploadImgServer =
```

### 方法
```
this.$refs.editor.getHtml()
this.$refs.editor.setHtml()
```