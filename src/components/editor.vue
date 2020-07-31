<template>
  <div class="editor">
    <div class="editor-menu">
      <div class="editor-button-content" style="grid-column-start: 1;grid-column-end: 3;">
        <div style="border: 1px solid #cccccc;background: #fff;padding: 10px;">
          <div class="span-image-content">
            <img src="./upload.png" class="span-image-upload" @click="imageFile" />
            <img
              class="span-image"
              onmousedown="return false"
              v-for="(item,index) in imageList"
              :key="index"
              :src="item"
              @click="imageSelect(item)"
            />
          </div>
          <div style="display:none">
            <input
              ref="file"
              type="file"
              accept="image/jpg, image/jpeg, image/png, image/gif, image/bmp"
              @change="imageUpload"
            />
          </div>
        </div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="backColor">
          背景色
          <span
            class="span-color-select"
            :style="{background: backColorItem}"
            @click="backColorShow = !backColorShow"
          ></span>
        </div>
        <div class="editor-panle" v-show="backColorShow">
          <div class="span-color-content">
            <span
              class="span-color"
              :style="{background: item}"
              v-for="(item,index) in colorList"
              :key="index"
              @click="backColorSelect(item)"
            ></span>
          </div>
        </div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="foreColor">
          字颜色
          <span
            class="span-color-select"
            :style="{background: foreColorItem}"
            @click="foreColorShow = !foreColorShow"
          ></span>
        </div>
        <div class="editor-panle" v-show="foreColorShow">
          <div class="span-color-content">
            <span
              class="span-color"
              :style="{background: item}"
              v-for="(item,index) in colorList"
              :key="index"
              @click="foreColorSelect(item)"
            ></span>
          </div>
        </div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="fontName">字体</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="fontSize">字号</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="bold">加粗</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="italic">斜体</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="createLinkShowFn">添链接</div>
        <div class="editor-panle" v-show="createLinkShow">
          <input v-model="createLinkText" placeholder="链接文字" />
          <input v-model="createLinkItem" placeholder="https://" />
          <span class="editor-button-sure" @click="createLinkSure">确定</span>
        </div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="unlink">去链接</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="indent">添缩进</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="outdent">去缩进</div>
      </div>
      <!-- <div class="editor-button-content">
          <div class="editor-button" onmousedown="return false" @click="insertHTML">插入</div>
      </div>-->
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="insertOrderedList">有序</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="insertUnorderedList">无序</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="insertParagraph">添段落</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="insertText">纯文字</div>
      </div>

      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="justifyFull">两端对齐</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="justifyCenter">居中</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="justifyLeft">居左</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="justifyRight">居右</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="subscript">下角标</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="superscript">上角标</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="strikeThrough">中划线</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="underline">下划线</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="insertHorizontalRule">分隔线</div>
      </div>
      <!-- <div class="editor-button-content">
          <div class="editor-button" onmousedown="return false" @click="selectAll">全选</div>
        </div>
        <div class="editor-button-content">
          <div class="editor-button" onmousedown="return false" @click="copy">复制</div>
        </div>
        <div class="editor-button-content">
          <div class="editor-button" onmousedown="return false" @click="cut">剪切</div>
        </div>
        <div class="editor-button-content">
          <div class="editor-button" onmousedown="return false" @click="deleteFn">删除</div>
      </div>-->
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="removeFormat">去格式</div>
      </div>

      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="undo">上一步</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="redo">下一步</div>
      </div>
      <div class="editor-button-content">
        <div class="editor-button" onmousedown="return false" @click="lineHeightShowFn">行距</div>
        <div class="editor-panle" v-show="lineHeightShow">
          <div class="span-lineHeight-content">
            <span
              class="span-lineHeight"
              v-for="(item,index) in lineHeightList"
              :key="index"
              @click="lineHeightSelect(item)"
            >{{item}}</span>
          </div>
        </div>
      </div>
    </div>
    <div class="phone">
      <div class="editor-content" contenteditable="true"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "vueEditor",
  components: {},
  data() {
    return {
      // 背景色
      backColorShow: false,
      backColorItem: "#ef342a",

      // 链接
      createLinkShow: false,
      createLinkText: "",
      createLinkItem: "",

      // 字颜色
      foreColorShow: false,
      foreColorItem: "#ef342a",

      // 行高
      lineHeightShow: false,
      lineHeightItem: "",

      // 弹层，颜色列表
      colorList: [
        "#ef342a",
        "#f68f26",
        "#4ba946",
        "#0376c2",
        "#c077af",
        "#f8d29d"
      ],
      // 弹层，行间距列表
      lineHeightList: ["12px", "16px", "20px", "24px", "28px"],
      // 弹层，图片列表
      imageList: [
        "https://si.geilicdn.com/pcitem1276928634-691b000001734b284ff70a20b7b9_720_550.jpg.webp?w=160&h=160",
        "https://si.geilicdn.com/pcitem1276928634-691b000001734b284ff70a20b7b9_720_550.jpg.webp?w=160&h=160",
        "https://si.geilicdn.com/pcitem1276928634-691b000001734b284ff70a20b7b9_720_550.jpg.webp?w=160&h=160",
        "https://si.geilicdn.com/pcitem1276928634-691b000001734b284ff70a20b7b9_720_550.jpg.webp?w=160&h=160"
      ],

      uploadImgServer: "http://localhost:8080",
      // 当前的选区
      currentRange: ""
    };
  },
  methods: {
    setHtml(val) {
      document.getElementsByClassName("editor-content")[0].innerHTML = val;
    },
    getHtml() {
      return document.getElementsByClassName("editor-content")[0].innerHTML;
    },
    //  背景色
    backColor() {
      document.execCommand("backColor", false, this.backColorItem);
    },
    // 加粗
    bold() {
      document.execCommand("bold");
    },
    // 复制
    copy() {
      document.execCommand("copy");
    },
    // 添链接
    createLink() {
      document.execCommand("createLink", false, "www.baidu.com");
    },
    // 剪切
    cut() {
      document.execCommand("cut");
    },
    // 删除
    deleteFn() {
      document.execCommand("delete");
    },
    // 字体
    fontName() {
      document.execCommand("fontName");
    },
    // 字号
    fontSize() {
      document.execCommand("fontSize");
    },
    // 字颜色
    foreColor() {
      document.execCommand("foreColor", false, this.foreColorItem);
    },
    // 添缩进
    indent() {
      document.execCommand("indent");
    },
    // 分隔线
    insertHorizontalRule() {
      document.execCommand("insertHorizontalRule");
    },
    // 插入html
    insertHTML() {
      // 拼接 table 模板
      var r = void 0,
        rowNum = 5,
        colNum = 5,
        c = void 0;
      var html =
        '<table border="0" width="100%" cellpadding="0" cellspacing="0">';
      for (r = 0; r < rowNum; r++) {
        html += "<tr>";
        if (r === 0) {
          for (c = 0; c < colNum; c++) {
            html += "<th>&nbsp;</th>";
          }
        } else {
          for (c = 0; c < colNum; c++) {
            html += "<td>&nbsp;</td>";
          }
        }
        html += "</tr>";
      }
      html += "</table><p><br></p>";
      document.execCommand("insertHTML", true, html);
    },
    // 有序
    insertOrderedList() {
      document.execCommand("insertOrderedList");
    },
    // 无序
    insertUnorderedList() {
      document.execCommand("insertUnorderedList");
    },
    // 段落
    insertParagraph() {
      document.execCommand("insertParagraph");
    },
    // 纯文字
    insertText() {
      document.execCommand("insertText");
    },
    // 斜体
    italic() {
      document.execCommand("italic");
    },
    // 居中
    justifyCenter() {
      document.execCommand("justifyCenter");
    },
    // 两端对齐
    justifyFull() {
      document.execCommand("justifyFull");
    },
    // 居左
    justifyLeft() {
      document.execCommand("justifyLeft");
    },
    // 居右
    justifyRight() {
      document.execCommand("justifyRight");
    },
    // 去缩进
    outdent() {
      document.execCommand("outdent");
    },
    // 下一步
    redo() {
      document.execCommand("redo");
    },
    // 去格式
    removeFormat() {
      document.execCommand("removeFormat");
    },
    // 全选
    selectAll() {
      document.execCommand("selectAll");
    },
    // 中划线
    strikeThrough() {
      document.execCommand("strikeThrough");
    },
    // 下角标
    subscript() {
      document.execCommand("subscript");
    },
    // 上角标
    superscript() {
      document.execCommand("superscript");
    },
    // 下划线
    underline() {
      document.execCommand("underline");
    },
    // 上一步
    undo() {
      document.execCommand("undo");
    },
    // 去链接
    unlink() {
      document.execCommand("unlink");
    },

    // 自定义的方法
    // 选中背景色
    backColorSelect(item) {
      this.backColorItem = item;
      this.backColorShow = false;
    },
    // 显示a链接
    createLinkShowFn() {
      this.createLinkShow = !this.createLinkShow;
      this.createLinkText = "";
      this.createLinkItem = "";
      this.saveRange();
    },
    // 输入a链接
    createLinkSure() {
      this.createLinkShow = false;
      this.restoreSelection();
      document.execCommand(
        "insertHTML",
        false,
        '<a href="' +
          this.createLinkItem +
          '" target="_blank">' +
          this.createLinkText +
          "</a>"
      );
    },
    // 选中字颜色
    foreColorSelect(item) {
      this.foreColorItem = item;
      this.foreColorShow = false;
    },
    // 显示行间距
    lineHeightShowFn() {
      this.lineHeightShow = !this.lineHeightShow;
      this.lineHeightItem = "";
      this.saveRange();
    },
    // 选择行间距
    lineHeightSelect(item) {
      this.lineHeightItem = item;
      this.lineHeightShow = false;
      this.currentRange.startContainer.parentElement.style.lineHeight = this.lineHeightItem;
      this.restoreSelection();
    },
    // 选择图片
    imageSelect(item) {
      this.saveRange();
      // 有选区时插入图片
      if (this.currentRange) {
        //创建需要插入的元素
        var div = document.createElement("div");
        div.style.width = "100%";
        div.innerHTML = `<img src=${item} style="max-width:100%;"/>`;
        // 返回父节点为编辑器的根节点的当前元素
        var editElement = this.parentUntil(this.currentRange.startContainer);
        editElement && editElement.after(div);
        this.restoreSelection();
      }

      // this.currentRange.startContainer.parentElement.outerHTML =
      //   this.currentRange.startContainer.parentElement.outerHTML +
      //   `<div style="width: 100%"><img src=${item} style="max-width:100%;"/></div>`;
      //注意，此方法不能嵌套插入元素
      // document.execCommand(
      //   "insertHTML",
      //   false,
      //   `<p>1</p><img src=${item} style="max-width:100%;"/><p>2</p>`
      // );
      // document.execCommand(
      //   "formatBlock",
      //   false,
      //   '<h1>'
      // );
    },
    // 上传图片
    imageFile() {
      this.$refs.file.value = "";
      this.$refs.file.click();
    },
    // 网络上传
    imageUpload(e) {
      var files = e.target.files;
      if (!files || !files.length) {
        return;
      }
      // 添加图片数据
      var formdata = new FormData();
      for (var i = 0; i < files.length; i++) {
        formdata.append("file", files[i]);
      }

      // 服务地址
      // this.uploadImgServer =
      //   "http://192.168.15.215:31302/platformplugin/uploadFile.do";
      if (!this.uploadImgServer) {
        throw new Error("请配置上传图片的远程服务地址");
      }

      // 定义 xhr
      var xhr = new XMLHttpRequest();
      xhr.open("POST", this.uploadImgServer);
      // 返回数据
      xhr.onreadystatechange = () => {
        var result = "";
        if (xhr.readyState === 4) {
          if (xhr.status == 200) {
            result = xhr.responseText;
            try {
              result = JSON.parse(result);
            } catch (ex) {}
            // 将图片插入编辑器
            var data = result.datas || [];
            data.forEach(item => {
              this.insertLinkImg(item.url);
            });
          }
        }
      };
      // 发送请求
      xhr.send(formdata);
    },
    // 根据链接插入图片
    insertLinkImg(link) {
      if (!link) {
        return;
      }
      // 验证图片 url 是否有效，无效的话给出提示
      var img = document.createElement("img");
      img.onload = () => {
        this.imageList.unshift(link);
        img = null;
      };
      img.onerror = () => {
        // 无法成功下载图片
        console.log("图片错误");
        img = null;
        return;
      };
      img.onabort = () => {
        console.log("图片中断");
        img = null;
      };
      img.src = link;
    },

    // 找到编辑器根节点
    parentUntil(element) {
      var ele = element;
      if (ele.parentElement.className == "editor-content") {
        return ele;
      } else if (ele.tagName == "BODY") {
        return false;
      } else {
        return this.parentUntil(ele.parentElement);
      }
    },

    // 保存当前的选区
    saveRange(range) {
      if (range) {
        // 保存已有选区
        this.currentRange = range;
        return;
      }
      var selection = window.getSelection();
      console.log(selection);
      if (selection.rangeCount === 0) {
        console.log("请选区位置");
        return;
      }
      var range = selection.getRangeAt(0);
      console.log(range);

      // 当前焦点元素激活的是编辑区
      var contains = document
        .getElementsByClassName("editor-content")[0]
        .contains(range.commonAncestorContainer);
      if (contains) {
        this.currentRange = range;
      } else {
        console.log("请用鼠标选中需要插入位置");
      }
    },
    // 恢复选区
    restoreSelection() {
      var selection = window.getSelection();
      selection.removeAllRanges();
      selection.addRange(this.currentRange);
    }
  }
};
</script>


<style scoped>
.editor {
  display: grid;
  grid-template-columns: 300px 400px;
  grid-column-gap: 50px;
}
.editor-menu {
  display: grid;
  grid-template-columns: 150px 150px;
  grid-template-rows: 139px repeat(auto-fill, 41px);
}
.phone {
  background: url("./phone.png");
  background-size: 400px 800px;
  background-repeat: no-repeat;
}
.editor-content {
  border: 1px solid #cccccc;
  height: 600px;
  width: 372px;
  overflow-y: auto;
  background: #ffffff;
  margin: 100px auto;
}
.editor-content:focus {
  outline: none;
}
.editor-button-content {
  position: relative;
}
.editor-button {
  white-space: nowrap;
  cursor: pointer;
  background: #fff;
  border: 1px solid #dcdfe6;
  color: #606266;
  text-align: center;
  box-sizing: border-box;
  outline: 0;
  margin: 0;
  padding: 10px;
  font-size: 14px;
}

.editor-panle {
  position: absolute;
  z-index: 1;
  border: 1px solid #cccccc;
  background: #fff;
  padding: 10px;
}
.span-color-content {
  display: grid;
  grid-template-columns: 20px 20px 20px 20px 20px;
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}
.span-color-select {
  width: 12px;
  height: 12px;
  display: inline-block;
  background: #000;
}
.span-color {
  width: 20px;
  height: 20px;
  display: block;
  cursor: pointer;
  border: 1px solid #ffffff;
  background: #000;
}
.span-color:hover {
  border: 1px solid #1890ff;
}
.span-lineHeight {
  display: block;
  width: 60px;
  cursor: pointer;
  border: 1px solid #ffffff;
}
.span-lineHeight:hover {
  border: 1px solid #1890ff;
}
.span-image-content {
  overflow-x: scroll;
  white-space: nowrap;
}
.span-image {
  height: 100px;
  cursor: pointer;
  border: 1px solid #ffffff;
  margin: 0px 5px;
}
.span-image:hover {
  border: 1px solid #1890ff;
}
.span-image-upload {
  height: 100px;
  cursor: pointer;
  border: 1px solid #ffffff;
}
.editor-button-sure {
  color: #fff;
  display: inline-block;
  background: #409eff;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
