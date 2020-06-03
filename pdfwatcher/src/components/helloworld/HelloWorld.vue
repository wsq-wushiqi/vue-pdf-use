<template>
  <div class="main-container">
    <el-button @click="openPdf">打开</el-button>
    <el-dialog :visible.sync="pdfDlg" fullscreen title="pdf文件预览" width="800px" class="pdf-dialog">
      <iframe
        id="pdfiframe"
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
      currentPage: 1
    }
  },
  mounted() {
    sessionStorage.clear()
    // this.currentPage = 1
  },
  methods: {
    openPdf: function() {
      sessionStorage.setItem('page', 1)
      this.pdfDlg = true
      setTimeout(() => {
        this.$nextTick(() => {
          this.currentPage = sessionStorage.page
          let totalPage = sessionStorage.totalPage
        })
      }, 400);
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
.pdf-div {
  width: 100%;
  height: 100%;
  z-index: 180;
}
</style>
<style>
.pdf-dialog .el-dialog__body {
  height: 498px;
  padding: 10px;
}
</style>
