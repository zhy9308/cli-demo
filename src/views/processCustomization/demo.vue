<template>
  <div class="bpmn">
    <el-card class="box-card">
      <div class="bpmn-card">
        <div class="card-text">绘制流程</div> 
        <div class="canvas" ref="canvas" />
        <div class="toolbar">
          <a title="download" style="color:#333">下载</a>
          <a ref="saveDiagram" href="javascript:" title="download BPMN diagram">BPMN</a>
          <a ref="saveSvg" href="javascript:" title="download as SVG image">SVG</a>
        </div>
        <div class="btn">
      <el-button @click="confirm" type="primary" size="medium">确认</el-button>
      <el-button size="medium" @click="cancel">取消</el-button>
    </div>
          <!-- 通过判断有无bpmnModeler数据传参来控制显示和隐藏，传送bpmn实例数据（modeler,rootElment） -->
          <!-- <panel class="panel" v-if="bpmnModeler"  :modeler="bpmnModeler" /> -->
      </div>  
    </el-card>
  </div>
</template>

<script>
// 引入相关的依赖
import axios from "axios";  
import BpmnModeler from "bpmn-js/lib/Modeler"; // bpmn-js 设计器
// import panel from "./components/PropertyPanel.vue";
import BpmData from "@/assets/utils/BpmData.js";
import { xmlStr } from "@/assets/utils/xmlStr"; // 这里是直接引用了xml字符串

export default {
  data() {
    return {
      bpmnModeler: null,
      // element: null,
      bpmData: new BpmData(),
      // loading: true,
      selectedElements:[],
       xmlUrl: "",
       defaultXmlStr: xmlStr,
      // 渲染成图的bpmn
      rootElment:{},
      // 序列流事件
      // sequenceFlow:''
    };
  },
    components: {
    // panel,
  },
  created() {},
  mounted() {
     this.init();
       // 获取到属性ref为“canvas”的dom节点
      const canvas = this.$refs.canvas;
      // 建模
      this.bpmnModeler = new BpmnModeler({
        container: canvas,
      });
      this.createNewDiagram();
  },
  watch: {},
  methods: {
     async init() {
      this.xmlUrl = await this.getXmlUrl();
      // this.$nextTick(() => {
      //   this.initBpmn();
      // });
    },
    getXmlUrl() {
      return new Promise(resolve => {
        setTimeout(() => {
          // const url = 'https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/mock1.bpmn'
          const url = "";
          resolve(url);
        }, 300);
      });
    },
     // 初始化bpmn
    // initBpmn() { 
    // },
      // 创建新图表
    async createNewDiagram() {
      const that = this;
      let bpmnXmlStr = "";
      // 如果请求地址为空就传送原xml代码
      if (this.xmlUrl === "") {
        bpmnXmlStr = this.defaultXmlStr;
        this.transformCanvas(bpmnXmlStr);
      } else {
        // 请求后台bpmn的xml格式代码
        let res = await axios({
          method: "get",
          timeout: 120000,
          url: that.xmlUrl,
          headers: { "Content-Type": "multipart/form-data" }
        });
        bpmnXmlStr = res["data"];
        // 把请求过来的代码传给函数
        this.transformCanvas(bpmnXmlStr);
      }
    },
    // 将字符串转换成图并渲染
    transformCanvas(bpmnXmlStr) {
      this.bpmnModeler.importXML(bpmnXmlStr, err => {
        if (err) {
          console.error(err);
        } else {
          this.success();
          this.adjustPalette();
        }
        // 让图能自适应屏幕
        var canvas = this.bpmnModeler.get("canvas");
        canvas.zoom("fit-viewport");
      });
    },
       // 调整左侧工具栏排版
    adjustPalette() {
      try {
        // 获取 bpmn 设计器实例
        const canvas = this.$refs.canvas;
        const djsPalette = canvas.children[0].children[1].children[4];
        const djsPalStyle = {
          width: "110px",
          padding: "2px",
          background: "white",
          left: "20px",
          borderRadius: 0
        };
        for (var key in djsPalStyle) {
          djsPalette.style[key] = djsPalStyle[key];
        }
        const palette = djsPalette.children[0];
        const allGroups = palette.children;
        allGroups[0].style["display"] = "none";
        // 修改控件样式
        for (var gKey in allGroups) {
          const group = allGroups[gKey];
          for (var cKey in group.children) {
            const control = group.children[cKey];
            const controlStyle = {
              display: "flex",
              justifyContent: "flex-start",
              alignItems: "center",
              width: "100%",
              padding: "2px",
              fontSize: "24px",
              height: "26px"
            };
            if (
              control.className &&
              control.dataset &&
              control.className.indexOf("entry") !== -1
            ) {
              const controlProps = this.bpmData.getControl(
                control.dataset.action
              );
              control.innerHTML = `<div style='font-size: 14px;font-weight:500;margin-left:15px;'>${controlProps["title"]}</div>`;
              for (var csKey in controlStyle) {
                control.style[csKey] = controlStyle[csKey];
              }
            }
          }
        }
      } catch (e) {
        console.log(e);
      }
    },
     success() {
      console.log("创建成功!");
      this.addBpmnListener();
      this.addModelerListener();
    },
     // 添加绑定事件
    addBpmnListener() {
      const that = this;
      // 获取a标签dom节点
      const downloadLink = this.$refs.saveDiagram;
      const downloadSvgLink = this.$refs.saveSvg;
      // 给图绑定事件，当图有发生改变就会触发这个事件
      this.bpmnModeler.on("commandStack.changed", function() {
        // 如果捕获正确信息就返回svg代码，返回错误信息就返回错误信息err
          // diagram.svg 文件名
        that.saveSVG(function(err, svg) {
          that.setEncoded(downloadSvgLink, "diagram.svg", err ? null : svg);
        });
        that.saveDiagram(function(err, xml) {
          that.setEncoded(downloadLink, "diagram.bpmn", err ? null : xml);
        });
      });
      // console.log(this.bpmnModeler);
      
    },
    // 添加建模者监听器
    addModelerListener() {
      const bpmnjs = this.bpmnModeler;
      // 获取bpmn原型上的第一条定义
      // const rootElment = (this.bpmnModeler.getDefinitions().rootElements[0]) 
      const that = this;
      // 'shape.removed'
      const events = [
        "shape.added", //添加事件
        "shape.move.end", //移动终点
        "connect.end", //连接结束
        "connection.create", //连接创建
        "connection.move" //连接移动
      ];
      // 循环并监听事件
      events.forEach(function(event) {
        that.bpmnModeler.on(event, e => {
          // console.log(e)
          var elementRegistry = bpmnjs.get("elementRegistry");// 获取元素登记
          // console.log(elementRegistry);
          var shape = e.element ? elementRegistry.get(e.element.id) : e.shape; //如果有元素就获取事件元素就获取元素的id，否则返回元素形状
          // console.log(shape);                                                                                                                                                                                                                                                                                                                     
          
        }); 
      });
    },
     // 下载为SVG格式,done是个函数，调用的时候传入的
    saveSVG(done) {
      // console.log(done); 
      // 把传入的done再传给bpmn原型的saveSVG函数调用
      this.bpmnModeler.saveSVG(done);
    },
     // 下载为bpmn格式,done是个函数，调用的时候传入的
    saveDiagram(done) {
      // 把传入的done再传给bpmn原型的saveXML函数调用
      this.bpmnModeler.saveXML({ format: true }, function(err, xml) {
        done(err, xml);
      });
    },
    confirm() {},
    cancel(){},
   
     // 当下载的时候会调用这个函数，link 是a标签dom，name是文件名字，这个data就是图的xml
    setEncoded(link, name, data) {
      // 把xml转换为URI，下载要用到的
      const encodedData = encodeURIComponent(data);
      // 下载图的具体操作,改变a的属性，className令a标签可点击，href令能下载，download是下载的文件的名字
      let xmlFile = new File([data], "test.bpmn");  
      if (data) {
        link.className = "active";
        link.href = "data:application/bpmn20-xml;charset=UTF-8," + encodedData;
        link.download = name;
      }
    },
   
  },

};
</script>

    <style scoped lang="scss">
/*左边工具栏以及编辑节点的样式*/
// @import "~bpmn-js/dist/assets/diagram-js.css";
// @import "~bpmn-js/dist/assets/bpmn-font/css/bpmn.css";
// @import "~bpmn-js/dist/assets/bpmn-font/css/bpmn-codes.css";
// @import "~bpmn-js/dist/assets/bpmn-font/css/bpmn-embedded.css";
.bpmn {
  background-color: #ffffff;
  width: 100%;
  height: 800px;
  position: relative;
  .box-card {
    height: 680px;
    height: 100%;

    .card-text {
      font-size: 18px;
    }
  }
  .canvas {
    width: 100%;
    height: 100%;
  }
  .entry {
    height: 40px;
    z-index: 999;
  }
  // .panel {
  //   position: absolute;
  //   right: 0;
  //   width: 300px;
  // }
  .bpmn-card {
    height: 24.8rem;
    width: 100%;
  }
  .toolbar {
    position: absolute;
    top: 20px;
    right: 350px;
    a {
      text-decoration: none;
      margin: 5px;
      color: #409eff;
      font-size: 16px;
    }
  }
  // .btn {
  //   display: flex;
  //   justify-content: flex-end;
  //   margin-right: 30px;
  //   margin-bottom: 20px;
  //   margin-top: -20px;
  // }
  .card {
    height: 80%;
    position: relative;
  }
  .el-input {
    position: relative;
  }
  .btn {
  display: flex;
  position: absolute;
  top:8px;
  right: 30px;
  margin-bottom: 40px;
  justify-content: flex-end;
}
  .addImg {
    position: absolute;
    right: 12px;
    top: 10px;
    width: 16px;
    height: 18px;
  }
  /*隐藏bpmnjs图标*/
  .bjs-powered-by {
    display: none !important;
  }
}
</style>
