<template>
  <div class="form_delivery">
    <div class="delivery_details">
      <span class="text_color" style="font-size: 35px;">Delivery details</span>
      <span> <input type="checkbox" name="isCheck" id="check" v-model="isDropshipChecked" @change="isDropToogle"> Send as dropshipper</span>
    </div>
    <div class='some-page-wrapper'>
      <div class='row'>
        <div class='column'>
          <div class='blue-column'>
            <input type="text" class="custom-input" placeholder="Name" @input="emitData" v-model="formDelivery.name" />
          </div>
        </div>
        <div class='column'>
          <div class='green-column'>
            <input type="text" class="custom-input" placeholder="Dropshipper Name" @input="emitData" :disabled="!isDropshipChecked" v-model="formDelivery.dropshipper_name" />
          </div>
        </div>
      </div>
      <div class='row'>
        <div class='column'>
          <div class='blue-column'>
            <input type="number" class="custom-input" placeholder="Phone Number" @input="emitData" v-model="formDelivery.phone_number" />
          </div>
        </div>
        <div class='column'>
          <div class='green-column'>
            <input type="text" class="custom-input" placeholder="Dropshipper Phone Number" @input="emitData" :disabled="!isDropshipChecked" v-model="formDelivery.dropshipper_phone_number" />
          </div>
        </div>
      </div>
      <div class='row'>
        <div class='column'>
          <div class='blue-column'>
            <input type="text" class="custom-input" placeholder="Delivery Address" @input="emitData" v-model="formDelivery.address" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DeliveryDetails',
  data() {
    return {
      formDelivery: {
        name: '',
        dropshipper_name: '',
        phone_number: '',
        dropshipper_phone_number: '',
        address: ''
      },
      isDropshipChecked: false
    }
  },
  methods: {
    emitData() {
      this.$emit('input', this.formDelivery)
    },
    isDropToogle() {
      this.$emit('isDrop', this.isDropshipChecked)
    }
  },
}
</script>
<style lang="stylus" scoped>
.form_delivery
  diplay flex
  flex-direction column
.delivery_details
  width 90%
  display flex
  justify-content space-between
  margin-bottom 20px
.text_color
  color #FF8A00
  font-weight bold
.custom-input
  margin-bottom 10px
  border 1px solid #ccc
  padding 15px
  font-size 20px
  color #333
  min-width 350px
  height 60px
  &:focus
    outline none
    border-color #ccc
.row
  display: flex
  flex-direction: row
  flex-wrap: wrap
  width: 100%
.column
  display: flex
  flex-direction: column
  flex-basis: 100%
  flex: 1
</style>