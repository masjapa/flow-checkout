<template>
  <div>
    <div>
      <span class="text_color" style="font-size: 35px;">Shipment</span>
    </div>
    <div class="section">
      <div v-for="(item, index) in shipment" :key="index" class="box" @click="addShipment(item.name)">
        <div>
          {{ item.name }}
        </div>
        <div class="price_tag">
          {{  item.price }}
        </div>
      </div>
    </div>
    <div>
      <span class="text_color" style="font-size: 35px;">Payment</span>
    </div>
    <div class="section">
      <div v-for="(item, index) in payment" :key="index" class="box" @click="addPayment(item.name)">
        <div>
          {{ item.name }}
        </div>
        <div class="price_tag" v-if="item.amount > 0">
          {{  item.amount }} left
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'PaymentDetails',
  data() {
    return {
      shipment: [
        {
          name: 'GO-SEND',
          price: 15000
        },
        {
          name: 'JNE',
          price: 9000
        },
        {
          name: 'Personal Courier',
          price: 29000
        }
      ],
      payment: [
        {
          name: 'e-Wallet',
          amount: 1500000
        },
        {
          name: 'Bank Transfer',
          amount: 0
        },
        {
          name: 'Virtual Account',
          amount: 0
        }
      ]
    }
  },
  methods: {
    addShipment(val) {
      console.log(val)
    },
    addPayment(val) {
      console.log(val)
    }
  },
}
</script>
<style lang="stylus" scoped>
.section
  display flex
  gap 10px
  margin 10px 0
.price_tag
  font-weight bold
.text_color
  color #FF8A00
  font-weight bold
.box
  padding 15px
  border 1px solid grey
  width 180px
  cursor pointer
</style>