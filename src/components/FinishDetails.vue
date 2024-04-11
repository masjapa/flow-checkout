<template>
  <div class="finish_section">
    <div class="indent">
      <span class="text_color">Thank You</span>
      <div class="inner">
        <span>Order ID : {{ code }}</span>
        <span>Your order will be delivered with {{ deliver }}</span>
      </div>
      <span>Go To Homepage</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'FinishDetails',
  props: ['code', 'deliver'],
  data() {
    return {
    }
  }
}
</script>
<style lang="stylus" scoped>
.finish_section
  display flex
  height 100%
  justify-content center
  align-items center
.indent
  display flex
  flex-direction column
  gap 30px
.inner 
  display flex
  flex-direction column
.text_color
  font-size 35px
  color #FF8A00
  font-weight bold
</style>