<template>
  <div class="zujian-list" draggable="true" @dragstart.capture="dragstarthandle(list, index, $event)" @drop.stop="drophandle(list, index, $event)" @dragover.prevent="dragoverhandle(list, index, $event)">
    <div v-if="list.type === '1'">
       轮播图
    </div>
    <div v-if="list.type === '2'">
      图片
    </div>
    <div v-if="list.type === '3'">
      文字
    </div>
    <div v-if="list.type === '4'">
      商家
    </div>
    <div v-if="list.type === '5'">
      卡券
    </div>
  </div>
</template>

<script>
export default {
  name: 'zujian-list',
  data () {
    return {
    }
  },
  props: {
    index: '',
    draglist: {
      type: Array
    },
    zujianlist: {
      type: Array
    },
    list: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  methods: {
    dragstarthandle (item, index, e) {
      e.dataTransfer.setData('index', index)
    },
    drophandle (item, index, e) {
      var getIndex = e.dataTransfer.getData('index')
      if (getIndex.startsWith('zujian')) {
        const i = getIndex.substring(6)
        this.draglist.splice(++index, 0, this.zujianlist[i])
        return ''
      } else {
        const needpushitem = this.draglist.splice(getIndex, 1)[0]
        this.draglist.splice(index, 0, needpushitem)
      }
    },
    dragoverhandle (item, index, e) {}
  },
  created () {
    console.log(typeof this.list.type)
  }
}
</script>

<style scoped>
.zujian-list div{
  width:100%;
  height:60px;
  background:#81c7d4;
  line-height:60px;
  text-align: center;
  border-bottom: 1px solid yellow;
}
</style>
