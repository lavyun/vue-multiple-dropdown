<template>
  <div id="app">
    <p>select</p>
    <p>value1:{{value1}}</p>
    <p>value2:{{value2}}</p>
    <p>value3:{{value3}}</p>
    <multi-dropdown>
      <multi-dropdown-item title="时间" :list="list1" v-model="value1"></multi-dropdown-item>
      <multi-dropdown-item title="地点" :list="list2" v-model="value2" icon-class="iconfont icon-danxuanon"></multi-dropdown-item>
      <multi-dropdown-item title="人物" :list="list3" v-model="value3"></multi-dropdown-item>
    </multi-dropdown>
  </div>
</template>

<script>
  import {MultiDropdown, MultiDropdownItem} from 'vue-multiple-dropdown'

  export default {
    name: 'app',
    components: {
      MultiDropdown,
      MultiDropdownItem
    },
    data(){
      return {
        list1: ['星期一', '星期二', '星期三', '星期四'],
        list2: ['北京', '上海', '杭州'],
        list3: ['奥巴马', '侯亮平', '周杰伦'],
        value1: '星期一',
        value2: '上海',
        value3: ''
      }
    }
  }
</script>

<style>
  * {margin: 0; padding: 0}
  #app{width: 375px;height: 675px;border: 1px solid palevioletred;margin: 100px auto}
  body{background-color: #e4e4e4}
</style>
