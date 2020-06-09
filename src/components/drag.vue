<template>
  <div class="full-page">
    <grid-layout
      :layout.sync="layout"
      :col-num="12"
      :row-height="30"
      :is-draggable="draggable"
      :is-resizable="resizable"
      :is-mirrored="false"
      :vertical-compact="true"
      :margin="[8, 8]"
      :use-css-transforms="true"
      @layout-created="layoutCreatedEvent"
      @layout-before-mount="layoutBeforeMountEvent"
      @layout-mounted="layoutMountedEvent"
      @layout-ready="layoutReadyEvent"
      @layout-updated="layoutUpdatedEvent"
    >
      <grid-item v-for="item in layout"
        :x="item.x"
        :y="item.y"
        :w="item.w"
        :h="item.h"
        :i="item.i"
        :min-w="2"
        :min-h="4"
        :is-draggable="item.h !== 6"
        :is-resizable="item.i !== '3'"
        :key="item.i"
        @resize="resizeEvent"
        @move="moveEvent"
        @resized="resizedEvent"
        @moved="movedEvent"
      >
        <div v-if="item.h === 6">不可拖拽</div>
        <div v-else-if="item.i === '3'">不可改变</div>
        <div v-else>{{item.i}}</div>
      </grid-item>
    </grid-layout>
    <!-- 全局设置, 需要取消 grid-item 拖拽,改变项 -->
    <div class="btn-warpper">
      <button
        @click="draggable === true ? draggable = false : draggable = true"
      >{{ draggable === true ? '可拖' : '不可' }}</button>
      <button
        @click="resizable === true ? resizable = false : resizable = true"
      >{{ resizable === true ? '可改' : '不可' }}</button>
    </div>
  </div>
</template>
<script>
/**
 * @author 🌈MARS <wangdaoo66@gmail.com>
 * @desc 📝拖拽组件示例
 * @copyright 🤝2020 尽人事, 行王道
 * @see https://github.com/jbaysolutions/vue-grid-layout/blob/master/README-zh_CN.md
 * @desc 如果给 grid-item 单独设置了是否可拖拽,可改变, 则父元素设置无效
 */
import { GridLayout, GridItem } from 'vue-grid-layout'
export default {
  name: 'Drag',
  components: {
    GridLayout,
    GridItem
  },
  data: () => ({
    layout: [
      {"x":0,"y":0,"w":2,"h":5,"i":"0"},
      {"x":2,"y":0,"w":2,"h":4,"i":"1"},
      {"x":4,"y":0,"w":2,"h":5,"i":"2"},
      {"x":6,"y":0,"w":2,"h":4,"i":"3"},
      {"x":8,"y":0,"w":2,"h":7,"i":"4"},
      {"x":10,"y":0,"w":2,"h":6,"i":"5"},
      {"x":0,"y":5,"w":2,"h":4,"i":"6"},
      {"x":2,"y":5,"w":2,"h":4,"i":"7"},
      {"x":4,"y":5,"w":2,"h":6,"i":"8"},
      {"x":6,"y":3,"w":2,"h":4,"i":"9"},
      {"x":8,"y":4,"w":2,"h":4,"i":"10"},
      {"x":10,"y":4,"w":2,"h":4,"i":"11"},
      {"x":0,"y":10,"w":2,"h":5,"i":"12"},
      {"x":2,"y":10,"w":2,"h":5,"i":"13"},
      {"x":4,"y":8,"w":2,"h":4,"i":"14"},
      {"x":6,"y":8,"w":2,"h":4,"i":"15"},
      {"x":8,"y":10,"w":2,"h":5,"i":"16"},
      {"x":10,"y":4,"w":2,"h":5,"i":"17"},
      {"x":0,"y":9,"w":2,"h":5,"i":"18"},
      {"x":2,"y":6,"w":2,"h":4,"i":"19"}
    ],
    draggable: true,
    resizable: true
  }),

  mounted () {

  },  

  methods: {
    /**获取渲染数据 */
    layoutCreatedEvent (layout) {
      console.group(`%c create`, 'color: #2ecc71; font-size: 14px;')
      console.log(layout)
      console.groupEnd()
    },
    /**渲染之前 */
    layoutBeforeMountEvent (layout) {
      console.group(`%c beforeMount`, 'color: #2ecc71; font-size: 14px;')
      console.log(layout)
      console.groupEnd()
    },
    /**数据渲染 */
    layoutMountedEvent (layout) {
      console.group(`%c mounted`, 'color: #2ecc71; font-size: 14px;')
      console.log(layout)
      console.groupEnd()
    },
    /**完成操作时 */
    layoutReadyEvent (layout) {
      console.group(`%c ready`, 'color: #2ecc71; font-size: 14px;')
      console.log(layout)
      console.groupEnd()
    },
    /**布局更新重新计算 */
    layoutUpdatedEvent (layout) {
      console.group(`%c update`, 'color: #2ecc71; font-size: 14px;')
      console.log(layout)
      console.groupEnd()
    },

    // !grid-item 事件 👇
    /**
     * @func grid-item事件
     * @param {String} i 唯一标识
     * @param {Number} newX x轴位置
     * @param {Number} newY y轴位置
     * @param {Number} newH 改变后高, 对应原始数据 h
     * @param {Number} newW 改变后宽, 对应原始数据 w
     * @param {Number} hPx 改变后高度, 像素级
     * @param {Number} wPx 改变后宽度, 像素级
     */
    /**移动时 */
    moveEvent (i, newX, newY) {
      console.log("MOVE i=" + i + ", X=" + newX + ", Y=" + newY)
    },
    /**调整大小 */
    resizeEvent (i, newH, newW, hPx, wPx) {
      console.log("RESIZE i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + hPx + ", W(px)=" + wPx)
    },
    /**移动完成 */
    movedEvent (i, newX, newY) {
      console.log("MOVED i=" + i + ", X=" + newX + ", Y=" + newY)
    },

    /**调整完成 */
    resizedEvent (i, newH, newW, hPx, wPx) {
      console.log("RESIZED i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + hPx + ", W(px)=" + wPx)
    },

  }
}
</script>
<style lang="css" scoped>
.vue-grid-item {
  background:#ecf0f1;
}
.vue-grid-item:nth-child(4) {
  background: yellow;
}
.vue-grid-item:nth-child(6) {
  background: red;
}
.vue-grid-item:nth-child(9) {
  background: red;
}
.vue-grid-item > div {
  font-size: 30px;
  text-align: center;
}
.full-page {
  width: 100%;
  height: 100vh;
  background: #232526;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #414345, #232526);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #414345, #232526); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.btn-warpper {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 80px;
  height: 80px;
  /* background: #fff; */
}

.btn-warpper > button {
  width: 100%;
  height: 30px;
  margin-bottom: 6px;
}
</style>