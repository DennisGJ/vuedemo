<template>
  <div class="goods">
    <div class="search">
      <input type="text" placeholder="请输入搜索内容" class="search-content" v-model="search" @keyup="get($event)"
             @keydown.enter="searchInput()" @keydown.down="selectDown()" @keydown.up="selectUp()">
      <span class="search-reset" @click="clearInput">×</span>
      <button class="search-btn" @click="searchInput">搜索</button>
      <div class="search-select">
        <transition-group tag="ul" mode="out-in">
          <li v-for="(value,index) in myData" :class="{selectBg: index===now}" :key="index" @click="searchThis"
              @mouseover="selectHover(index)" class="search-select-list">{{value}}
          </li>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data() {
      return {
        search: '',
        myData: [],
        now: -1
      };
    },
    methods: {
      get: function (event) {
        if (event) {
          if (event.keyCode === 38 || event.keyCode === 40) {
            return;
          }
        }
        this.$http.jsonp('https://sug.so.360.cn/suggest?word=' + this.search + '&encodein=utf-8&encodeout=utf-8').then(response => {
          this.myData = response.body.s;
        }, response => {

        });
      },
      clearInput: function () {
        this.search = '';
        this.get();
      },
      searchInput: function () {
        window.open('https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=0&rsv_idx=1&tn=baidu&wd=' + this.search);
      },
      searchThis: function (index) {
        this.search = this.myData[index];
        this.searchInput();
      },
      selectHover: function (index) {
        this.search = this.myData[index];
        this.now = index;
      },
      selectDown: function () {
        this.now++;
        if (this.now === this.myData.length) {
          this.now = 0;
        }
        this.search = this.myData[this.now];
      },
      selectUp: function () {
        this.now--;
        if (this.now === -1) {
          this.now = this.myData.length - 1;
        }
        this.search = this.myData[this.now];
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .goods
    .search
      width: 300px
      height: 40px
      margin: 10px auto
      position: relative
      .search-content
        width: 200px
        height: 40px
        border: 1px solid #ccc
        box-sizing: border-box
        float: left
        outline: none
        padding: 0 40px 0 10px
      .search-reset
        position: absolute
        display: inline-block
        width: 20px
        height: 20px
        right: 110px
        top: 11px
        font-size: 20px
        line-height: 20px
        text-align: center
        cursor: pointer
      .search-btn
        width: 100px
        height: 40px
        float: left
        background: skyblue
        border: 1px solid skyblue
        box-sizing border-box
        font-size: 18px
        outline: none
      .search-select
        ul
          .search-select-list
            padding-left: 10px
            border-left: 1px solid #ccc
            border-right: 1px solid #ccc
            line-height: 30px
            transition: all 0.5s
            &:last-child
              border-bottom: 1px solid #ccc
            &.selectBg
              background: #ccc
</style>
