<template>
  <div class="main-container">
    <el-button @click="openPdf">打开</el-button>
    <el-dialog :visible.sync="pdfDlg" fullscreen title="pdf文件预览" width="800px" class="pdf-dialog">
      <div class="check" @click="choosePage">
        <img
          v-if="check[currentPage]"
          style="width: 100px; height: 100px"
          src="../assets/check.png"
           />
        <img
          v-else
          style="width: 100px; height: 100px"
          src="../assets/unCheck1.png"
           />
      </div>
      <iframe
        id="pdf-iframe"
        ref="pdfIframe"
        :src="'/static/pdf/web/viewer.html?file=' + 'https://dakaname.oss-cn-hangzhou.aliyuncs.com/file/2018-12-28/1546003237411.pdf'"
        class="pdf-viewer"
        >
      </iframe>
      <div class="pdf-footer">
        <el-button @click="pdfDlg = false">关闭</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pdfDlg: false,
      check: [],
      currentPage: ''
    }
  },
  mounted() {
    this.currentPage = sessionStorage.page
    console.log(this.currentPage);
    
  },
  methods: {
    openPdf: function() {
      this.pdfDlg = true
    },
    choosePage: function() {
      console.log(1111111);
      // console.log(this.$refs.pdfIframe);
      // let currentPage = 0
      // let iFrame = document.getElementById('pdf-iframe')
      // console.log(JSON.parse(localStorage.getItem('pdfjs.history')).files[0].page);
      console.log(sessionStorage.page);
      this.currentPage = sessionStorage.page
      this.check[sessionStorage.page] = true
      console.log(this.check);
      
      // if (iFrame.contentDocument) {
      //   currentPage = iFrame.contentDocument.getElementById
      // }
    },
  watch: {
    'check': {
      handler: function(val, oldval) {
        console.log(val);
        console.log(oldval);
        
      }
    }
  }
  }
}
</script>

<style scoped>
.pdf-viewer {
  width: 100%;
  height: 100%;
}
.pdf-footer {
  bottom: 0;
  display: flex;
  margin: 0px 0px 5px 0px;
  z-index: 300;
  list-style: none;
  background-color: #797c782f;
  height: 50px;
}
.check {
  /* background-color: #ffffff; */
  width: 100px;
  height: 100px;
  position: fixed;
  z-index: 200;
  top: 120px;
  left: 20px;
}
</style>
<style>
.pdf-dialog .el-dialog__body {
  height: 700px;
  padding: 10px;
}
/* .pdf-dialog .el-dialog__footer {
  bottom: 0;
  display: flex;
  margin: 0px 0px 5px 0px;
  z-index: 300;
  list-style: none;
  background-color: #797c782f;
  height: 50px;
} */
</style>