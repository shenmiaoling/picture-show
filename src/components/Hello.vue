<style lang="styl" scoped>
.input-area
  position: absolute;
  z-index: 2;
.area
  width: 100%;
  height: 100%;
  opacity 0
.picture img
  position: absolute;
.panel {
  position: fixed;
  width: 100%;
  left: 0;
  right: 0;
  top 80px
}
.fix-panel
  position: fixed;
  width: 100%;
  left: 0;
  right: 0;
  top 80px
  z-index 3
.cover-panel
  position: absolute;
  opacity 0
  z-index 5
.picture {
  position:absolute;
  left:0px;top:0px;
  height:100%;
  width:100%;
  z-index: 1
}
.cover-top
  width: 100%;
  height: 80px;
  position: absolute;
  background: #ffffff;
  top: 0;
  z-index: 100;
.cover-bottom
  position: fixed;
  width: 100%;
  height: 100%;
  bottom: 0;
  background #ffffff
  z-index 100
button
  position absolute
  z-index 110
  /*border none*/
</style>
<template>
<div>
  <div class="cover-top"></div>
  <img src="../assets/bg3.png" :class="{'panel':!zIndex,'fix-panel':zIndex }">
  <div class="cover-bottom" :style="{'top': coverTop+'px'}"></div>
    <div class="input-area" :style="{'top': imageTop+'px', 'left': imageLeft+'px','width': imageWidth+'px','height': imageHeight+'px'}">
      <input class="area" type="file" accept="image/*" @change="addPicture">
    </div>
    <div class="picture" id="picture">
      <img id="output" :style="{'top': imageTop+'px', 'left': imageLeft+'px','width': imageWidth+'px'}">
    </div>
    <div class="cover-panel" id="cover" v-show="zIndex" :style="{'top': imageTop+'px', 'left': imageLeft+'px','width': imageWidth+'px','height': imageHeight+'px'}"></div>
    <button @click="computePosition">图片位置</button>
</div>
</template>

<script>
import interact,{dragMoveListener} from 'interactjs'
import nvDragging from './Dragging.vue'
export default {
  name: 'hello',
  data () {
    return {
      zIndex: false,
      imageTop: 10,
      imageLeft: 10,
      imageWidth: 0,
      imageHeight: 0,
      coverTop: 0
    }
  },
  mounted() {
  //获取元素
  this.imageWidth = 1276*window.innerWidth/3300
  this.imageLeft = 1686*window.innerWidth/3300
  this.imageTop = 630*window.innerWidth/3300+80
  this.imageHeight = 1298*window.innerWidth/3300
  this.coverTop = 2550*window.innerWidth/3300+80
  var photo=document.getElementById("output")
  var picture=document.getElementById("cover");
  //添加触屏开始事件
  picture.addEventListener("touchstart",function(e){
    var p,f1,f2;
    //由于触屏的坐标是个数组，所以取出这个数组的第一个元素
    e=e.touches[0];
    //保存picture和开始触屏时的坐标差
    p={
      x:picture.offsetLeft-e.clientX,
      y:picture.offsetTop-e.clientY
    };
    //添加触屏移动事件
    document.addEventListener("touchmove",f2=function(e){
      //获取保触屏坐标的对象
      var t=e.touches[0];
      var X = photo.getBoundingClientRect().left+document.documentElement.scrollLeft
      var Left = 1686*window.innerWidth/3300
      var Y =photo.getBoundingClientRect().top+document.documentElement.scrollTop;
        picture.style.left=p.x+t.clientX+"px";
        picture.style.top=p.y+t.clientY+"px";
        photo.style.left=p.x+t.clientX+"px";
        photo.style.top=p.y+t.clientY+"px";
    },false);
    //添加触屏结束事件
    document.addEventListener("touchend",f1=function(e){
      //移除在document上添加的两个事件
      document.removeEventListener("touchend",f1);
      document.removeEventListener("touchmove",f2);
    },false);
  },false);
  },
  methods:{
    addPicture(event) {
      this.zIndex = !this.zIndex
      var output = document.getElementById('output');
      output.src = URL.createObjectURL(event.target.files[0])
    },
  computePosition(){
    function getPosition(el) {
      var xPos = 0;
      var yPos = 0;
      while (el) {
        if (el.tagName == "BODY") {
          // deal with browser quirks with body/window/document and page scroll
          var xScroll = el.scrollLeft || document.documentElement.scrollLeft;
          var yScroll = el.scrollTop || document.documentElement.scrollTop;

          xPos += (el.offsetLeft - xScroll + el.clientLeft);
          yPos += (el.offsetTop - yScroll + el.clientTop);
        } else {
          // for all other non-BODY elements
          xPos += (el.offsetLeft - el.scrollLeft + el.clientLeft);
          yPos += (el.offsetTop - el.scrollTop + el.clientTop);
        }

        el = el.offsetParent;
      }
      return {
        x: xPos,
        y: yPos
      };
    }
    var myElement = document.querySelector("#output")
    var position = getPosition(myElement);
    console.log("The image is located at: " + position.x + ", " + position.y);
    }
  },
  components:{nvDragging}
}
</script>

