<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">商品</div>
      <div class="tab-item">评论</div>
      <div class="tab-item">商家</div>
    </div>
    <div class="content">
      I am content
    </div>
  </div>
</template>

<script>
import header from './components/header/header.vue'

const ERR_OK = 0

export default {
  data () {
    return {
      seller: {}
    }
  },

  created() {
    this.$http.get('api/seller').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
      }
    })
  },

  components: {
    'v-header': header
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scope>

  @import "common/scss/mixins";

  .tab {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    @include border-1px(rgba(7, 17, 27, 0.1));

    .tab-item {
      flex: 1;
      text-align: center;

      & > a {
        display: block;
        font-size: 14px;
        color: rgb(77, 85, 93);

        &.active {
          color: rgb(240, 20, 20)
        }
      }
    }
  }
</style>
