<template>
  <div class="main-container"  @mousewheel="pdfScroll">
    <el-button @click="openPdf">打开</el-button>
    <el-dialog :visible.sync="pdfDlg" fullscreen title="pdf文件预览" width="800px" class="pdf-dialog">
      <iframe
        id="pdfiframe"
        ref="pdfIframe"
        :src="'/static/pdf/web/viewer.html?file=' + 'https://dakaname.oss-cn-hangzhou.aliyuncs.com/file/2018-12-28/1546003237411.pdf'"
        class="pdf-viewer"
        onmousewheel="pdfScroll"
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
      currentPage: 1,
      testData: []
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
          for (let i = 1; i < totalPage; i++) {
            this.check[i] = false
          }
        })
      }, 400);
    },
    choosePage: function() {
      this.$forceUpdate()
      this.currentPage = sessionStorage.page
      if (this.check[this.currentPage]) {
        this.check[this.currentPage] = false
      } else {
        this.check[this.currentPage] = true
      }
      console.log(this.check);
    },
    pdfScroll: function() {
      console.log(9999999);
    },
    divClick: function() {
      console.log(22222);
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
  width: 100px;
  height: 100px;
  position: fixed;
  z-index: 200;
  top: 120px;
  left: 20px;
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