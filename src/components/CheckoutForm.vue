<template>
  <div>
    <div class="checkout_form">
      <StepperForm />
      <div class="back">
        <span v-if="step === 'deliveryStep'">Back to cart</span>
        <span v-if="step === 'paymentStep'" @click="nextStep('deliveryStep')">Back to delivery</span>
      </div>
      <div class="form_section">
        <div class="left_details">
          <DeliveryDetails v-if="step === 'deliveryStep'" />
          <PaymentDetails v-if="step === 'paymentStep'" />
          <FinishDetails v-if="step === 'finishStep'" />
        </div>
        <div class="summary_details">
          <div class="summary_items">
            <span class="text_color" style="font-size: 25px;">Summary</span>
            <span>10 Items Purchased</span>
          </div>
          <div class="summary_items">
            <div class="summary_sub">
              <span>Cost of goods</span>
              <span style="font-weight: bold;">500.000</span>
            </div>
            <div class="summary_sub">
              <span>Dropshipping Fee</span>
              <span style="font-weight: bold;">5.900</span>
            </div>
            <div class="summary_sub" style="font-size: 25px; margin-top: 20px;">
              <span class="text_color">Total</span>
              <span class="text_color">505.900</span>
            </div>
            <div>
              <input v-if="step === 'deliveryStep'" type="button" class="custom-button" value="Continue to Payment" @click="nextStep('paymentStep')">
              <input v-else-if="step === 'paymentStep'" type="button" class="custom-button" value="Pay with e-Wallet" @click="nextStep('finishStep')">
              <!-- <input v-else type="button" class="custom-button" value="Continue to Payment" @click="nextStep('deliveryStep')"> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DeliveryDetails from '@/components/DeliveryDetails.vue'
import StepperForm from '@/components/StepperForm.vue'
import PaymentDetails from '@/components/PaymentDetails.vue'
import FinishDetails from '@/components/FinishDetails.vue'
export default {
  name: 'CheckoutForm',
  components: {
    StepperForm,
    DeliveryDetails,
    PaymentDetails,
    FinishDetails
  },
  data() {
    return {
      step: localStorage.getItem('step'),
      inputForm: [
        {
          type: 'text',
          placeholder: 'Name'
        },
        {
          type: 'text',
          placeholder: 'Dropshipper Name'
        },
        {
          type: 'number',
          placeholder: 'Phone Number'
        },
        {
          type: 'number',
          placeholder: 'Dropshipper Phone Number'
        },
        {
          type: 'text',
          placeholder: 'Delivery Address'
        }
      ]
    }
  },
  methods: {
    nextStep(val) {
      this.step = val
      localStorage.setItem('step', this.step)
      if (this.step === 'finishStep') {
        localStorage.setItem('step', 'deliveryStep')
      }
    },
    prevStep() {
      
    }
  },
}
</script>
<style lang="stylus" scoped>
.back
  &:hover
    cursor pointer
.checkout_form
  margin 70px
  padding 40px
  background white
  border-radius 10px
  box-shadow 10px 20px 20px #979797
.form_section
  height 500px
  margin-top 30px
  display flex
  justify-content space-between
.left_details
  width 70%
.summary_details
  border-left 1px solid #FF8A00
  padding-left 10px
  width 30%
  display flex
  flex-direction column
  justify-content space-between
.summary_items
  display flex
  flex-direction column
.summary_sub
  display flex
  justify-content space-between
.text_color
  color #FF8A00
  font-weight bold
.custom-button
  margin-top 20px
  width 100%
  text-decoration none
  border none
  font-size 20px
  color white
  padding 20px
  background #FF8A00
  &:hover
    cursor pointer
</style>