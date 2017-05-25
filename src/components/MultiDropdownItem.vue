<template>
  <div multi-dropdown class="multiple-dropdown-item" :style="{width: itemWidth}">
    <div class="multiple-dropdown-item-wrap">
      <p class="md-title" @click="change">
        <span>{{title}}</span>
        <span class="iconfont icon-moreunfold" :class="{arrowToggle: show}"></span>
      </p>
      <ul multi-dropdown-list class="md-list" v-show="show" :style="{width: listWidth}">
        <li class="md-list-item" v-for="(item, index) in list" @click="select(index)">
          <p v-text="item"></p>
          <div class="md-list-icon-wrap" v-show="index === itemIndex">
            <span :class="iconClass" class="md-list-icon"></span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      title: String,
      value: [String, Number],
      iconClass:{
        type: String,
        default: 'iconfont icon-selected'
      },
      autoClose: {
        type: Boolean,
        default: true
      },
      list: {
        // Expected list is a Array of String and Number
        validator(list){
          if (!Array.isArray(list)) {
            return false;
          }
          for (let i of list) {
            if (typeof i !== 'string' && typeof i !== 'number') {
              return false;
            }
          }

          return true;
        }
      }
    },
    data(){
      return {
        itemWidth: null,
        show: false,
        listWidth: null,
        itemIndex: -1
      }
    },
    created(){
      this.itemIndex = this.list.indexOf(this.value)
    },
    mounted(){
      var parent = this.$el.parentNode;
      var items = parent.querySelectorAll('[multi-dropdown]');
      var itemsLength = items.length;
      this.itemWidth = 100 / itemsLength + '%';
      items[itemsLength - 1].style.border = "none";   // 最后一个item没有边框
      this.listWidth = parent.offsetWidth + 'px';
    },
    methods: {
      change(){
        if (this.show === true) {
          this.show = false;
          return;
        }
        if (this.show === false) {
          var itemSiblings = this.$parent.$children;  // 获取兄弟组件
          for (let i = 0; i < itemSiblings.length; i++) {
            itemSiblings[i].show = false;  // 隐藏兄弟组件的列表
          }
          this.show = true;
        }
      },
      select(index){
         this.itemIndex = index;
         if(this.autoClose) {
           setTimeout(()=>{
             this.show = false;
           }, 100)
         }
         this.$emit('input',this.list[index]);
      }
    }
  }
</script>
