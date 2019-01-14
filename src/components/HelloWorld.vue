<template>
  <div class="hello">
    <div class="content">
      <div v-for="(item,index) in zujianList" :key="index">
        <img :src="item.img" alt="" style="width:140px;height:140px;" draggable="true" @dragstart="dragstart(`zujian${index}`, $event)">
        <p>{{item.text}}</p>
      </div>
    </div>
    <div class="drag-box" @drop.self="onDrop($event)" @dragover.prevent="onDragover">
      <zujian-list v-for="(item,index) in dragList" :list="item" :key="index" :draglist.sync="dragList" :index="index" :zujianlist="zujianList"></zujian-list>
    </div>
  </div>
</template>

<script>
import zujianList from './zujian-list'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      zujianList: [
        {img: '../../static/images/1.jpg', text: '轮播图', type: '1'},
        {img: '../../static/images/2.jpg', text: '图片', type: '2'},
        {img: '../../static/images/3.jpg', text: '文字', type: '3'},
        {img: '../../static/images/4.jpg', text: '商家', type: '4'},
        {img: '../../static/images/5.png', text: '卡券', type: '5'}
      ],
      dragList: []
    }
  },
  components: {
    zujianList
  },
  methods: {
    dragstart (index, e) {
      e.dataTransfer.setData('index', index)
    },
    onDragover () {},
    onDrop (e) {
      var getIndex = e.dataTransfer.getData('index')
      console.log(getIndex)
      if (getIndex.length < 5) {
        console.log(this.dragList[getIndex])
        this.dragList.push(JSON.parse(JSON.stringify(this.dragList[getIndex])))
        this.dragList.splice(getIndex, 1)
        return ''
      }
      const i = getIndex.substring(6)
      this.dragList.push(JSON.parse(JSON.stringify(this.zujianList[i])))
    }
  },
  watch: {
    dragList (newValue) {
      console.log(newValue)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.content div {
  width:150px;
  height:180px;
  float:left;
  margin-right:30px;
}
  .content{
    width:500px;
    height:700px;
  }
  .drag-box{
    width:400px;
    height:600px;
    border: 1px solid red;
    position:absolute;
    left:500px;
    top:0;
    overflow: scroll;
  }
</style>
