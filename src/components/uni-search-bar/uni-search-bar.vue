<template>
  <view class="uni-searchbar">
    <view
      :class="show?'':'hide'"
      class="uni-searchbar-form" >
      <view
        :style="{borderRadius:radius+'rpx'}"
        class="uni-searchbar-form__box"
      >
        <uni-icons
          :color="'#999999'"
          class="icon-search"
          type="search"
          size="18"/>
        <input
          :placeholder="placeholder"
          :focus="show"
          v-model="searchVal"
          class="search-input"
          type="text"
          placeholder-style="color:#cccccc"
          confirm-type="search"
          @confirm="confirm">
        <uni-icons
          :color="'#999999'"
					v-if="clearButton==='always'||clearButton==='auto'&&searchVal!==''"
          class="icon-clear"
          type="clear"
          size="24"
          @click="clear"/>
      </view>
      <view
        :style="{borderRadius:radius+'rpx'}"
        class="uni-searchbar-form__text"
        @click="searchClick">
        <uni-icons
          color="#999999"
          class="icon-search"
          type="search"
          size="18"/>
        <text class="placeholder">{{ placeholder }}</text>
      </view>
      <text
        class="uni-searchbar-form__cancel"
        @click="cancel">取消</text>
    </view>
  </view>
</template>

<script>
import uniIcons from '../uni-icons/uni-icons.vue'
export default {
  name: 'UniSearchBar',
  components: {
    uniIcons
  },
  props: {
    placeholder: {
      type: String,
      default: '搜索'
    },
    radius: {
      type: [Number, String],
      default: 10
    },
    clearButton: {
      type: String,
      default: 'auto'
    }
  },
  data () {
    return {
      show: false,
      searchVal: ''
    }
  },
  watch: {
    searchVal () {
      this.$emit('input', { value: this.searchVal })
    }
  },
  methods: {
    searchClick () {
      this.searchVal = ''
      this.show = true
    },
    clear () {
      this.searchVal = ''
    },
    cancel () {
			this.$emit('cancel', { value: this.searchVal })
      this.searchVal = ''
      this.show = false
    },
    confirm () {
      this.$emit('confirm', { value: this.searchVal })
    }
  }
}
</script>

<style lang="scss">
  $uni-searchbar-height:64rpx;
  .uni-searchbar{
    &-form{
      position: relative;
      display: flex;
      padding: 15rpx;
      width: 100%;
      box-sizing: border-box;
      &__box{
        display: flex;
        flex: 1;
				align-items: center;
        width: 100%;
        height: $uni-searchbar-height;
        color: #c8c7cc;
        background: #ffffff;
        border: solid 1px #c8c7cc;
        border-radius: 10rpx;
        .icon-search{
          color: #c8c7cc;
          line-height: 24px;
          padding: 0rpx 10rpx 0rpx 15rpx;
        }
        .search-input{
          flex: 1;
          font-size: 28rpx;
          height: $uni-searchbar-height;
          line-height: $uni-searchbar-height;
          color: #333333;
        }
        .icon-clear{
          color: #c8c7cc;
          line-height: 20px;
          padding: 0rpx 15rpx 0rpx 10rpx;
        }
      }
      &__text{
        display: flex;
        flex: 1;
				align-items: center;
        width: 100%;
        height: $uni-searchbar-height;
        line-height: $uni-searchbar-height;
        text-align: center;
        color: #c8c7cc;
        background: #ffffff;
        border: solid 1px #c8c7cc;
        border-radius: 10rpx;
        display: none;
        .icon-search{
          height: $uni-searchbar-height;
          line-height: $uni-searchbar-height;
        }
        .placeholder{
          display: inline-block;
          font-size: 28rpx;
          color: #cccccc;
          margin-left: 10rpx;
        }
      }
      &__cancel{
        padding-left: 20rpx;
        line-height: $uni-searchbar-height;
        color: #333333;
				white-space: nowrap;
      }
      &.hide{
        .uni-searchbar-form__box{
          display: none;
        }
        .uni-searchbar-form__text{
          display: block;
        }
        .uni-searchbar-form__cancel{
          display: none;
        }
      }
    }
  }
</style>
