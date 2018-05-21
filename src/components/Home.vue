<template>
  <div id="app" class="content">
    <h1 class="todo__head">To-do App</h1>
    <!--{{ setItem }}-->
    <div class="todo__input-area">
      <input type="text" class="todo__input" autofocus v-model="inputValue" v-on:keyup.enter="addItem" placeholder="add new task">
    </div>
    <ul class="todo__list">
    <li v-for="(item, index) in items" class="todo__item" :class="{completed:item.completed}">
      <label class="todo__item-label" :class="{checked:item.completed}">
        <i class="fas fa-check"></i>
        <input type="checkbox" :id="'item'+ index" v-model="item.completed" class="todo__item-check">
      </label>
      <span class="todo__item-cont">{{ item.todo }}</span>
      <button type="button" @click="removeItem('item' + index)" class="todo__btn-delete"><i class="fas fa-trash-alt"></i></button>
    </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'home',
//    data() {
//      return {
//        msg: 'Welcome to Your Vue'
//      }
//    },
    data: function() {
      return {
        storageM: 'todos',
        inputValue: '',
        items: []
      }
    },
    created: function() {
      this.items = localStorage.getItem(this.storageM) ? JSON.parse(localStorage.getItem(this.storageM)) : [];
    },
//    computed: {
//      setItem: function() {
//        localStorage.setItem(this.storageM, JSON.stringify(this.items));
//      },
//    },
    watch: {
      items: {
        handler: function (val) {
          localStorage.setItem(this.storageM, JSON.stringify(this.items));
        },
        deep: true
      }
    },
    methods: {
      addItem : function() {
        if (this.inputValue) {
          this.items.push({'todo': this.inputValue, 'completed': false});
          this.inputValue = '';
        }
      },
      removeItem : function(i) {
        var index = i.replace('item','')
        this.items.splice(index,1);
      }
    }
  }

  // 기존 cdn 방식
  //var localCmp = {
  //  template: '<p>Hello vue</p>'
  //}
  //new Vue({
  //  data: {
  //
  //  },
  //  methods: {
  //
  //  }
  //});
</script>

<style lang="scss">
  .content {
    padding: 30px 40px;
  }
  .todo__ {
    &head {
      margin: 0;
      padding-bottom: 20px;
      font-size: 32px;
      font-weight: 500;
      color: #666;
      line-height: 1.45;
    }
    &input-area {
      padding: 0 40px 30px;
    }
    &input {
      display: block;
      width: 100%;
      border-style: solid;
      border-width: 0 0 2px;
      border-color:#cfcfcf;
      box-sizing: border-box;
      background-color: transparent;
      font-size: 28px;
      color: #666;
      letter-spacing: -1px;
      line-height:1.4;
      outline: 0;
    }
    &list {
      margin: 0;
    }
    &item {
      &.completed {
        .todo__ {
          &item-cont {
            color: #aaa;
            text-decoration: line-through;
          }
        }
      }
      position: relative;
      padding: 10px 40px;
      margin: 0;
      border-bottom: 1px solid #eee;
    }
    &item-label {
      &.checked {
        background: #eda680;
        background: -moz-linear-gradient(-45deg, #eda680 0%, #ef8234 100%);
        background: -webkit-linear-gradient(-45deg, #eda680 0%,#ef8234 100%);
        background: linear-gradient(135deg, #eda680 0%,#ef8234 100%);
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#eda680', endColorstr='#ef8234',GradientType=1 );
      }
      display: inline-block;
      position: absolute;
      top: 12px;
      left: 0;
      width: 20px;
      height: 20px;
      padding-top: 3px;
      border-radius: 12px;
      box-sizing: border-box;
      background-color: #dddedf;
      font-size: 12px;
      color: #fff;
      line-height: 1.4;
      vertical-align: top;
      text-align: center;
      cursor: pointer;
    }
    &item-check {
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      opacity: .01;
      cursor: pointer;
    }
    &item-cont {
      font-size: 16px;
      color: #666;
      line-height: 1.4;

    }
    &btn-delete {
      &:hover {
        border-color: #ff7f50;
        color: #ff7f50;
      }
      position: absolute;
      top: 9px;
      right: 0;
      width: 24px;
      height: 24px;
      border: 1px solid #eee;
      border-radius: 1px;
      font-size: 12px;
      color: #999;
      line-height: 22px;
      text-align: center;
      text-indent: -1px;
      cursor: pointer;
    }
  }
</style>
