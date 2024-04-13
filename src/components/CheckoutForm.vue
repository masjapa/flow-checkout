<template>
  <div>
    <div class="checkout-form">
      <StepperForm :deliveryStep="isDeliver" :paymentStep="isPayment" :finishStep="isFinish" />
      <div class="checkout-form__back">
        <span v-if="step === 'deliveryStep'">Back to cart</span>
        <span v-if="step === 'paymentStep'" @click="nextStep('deliveryStep')">Back to delivery</span>
      </div>
      <div class="checkout-form__section">
        <div class="checkout-form__left_details">
          <DeliveryDetails v-if="step === 'deliveryStep' || step === null" @input="handleForm" @isDrop="handleDrop" @isPhoneValid="handlePhoneNumber" @isPhoneDropshipValid="handlePhoneNumberDropship"/>
          <PaymentDetails v-if="step === 'paymentStep'" @selected-shipment="handleShipment" @selected-payment="handlePayment" />
          <FinishDetails v-if="step === 'finishStep'" :code="deliveryCode" :deliver="shipment" />
        </div>
        <div class="checkout-form__summary_details">
          <div class="checkout-form__summary_items">
            <span class="text_color" style="font-size: 25px;">Summary</span>
            <span>10 Items Purchased</span>
            <hr />
            <div>
              <div v-if="shipment || step === 'finishStep'">
                Delivery estimation
              </div>
              <div v-if="shipment === 'GO-SEND'">
                <span style="color: #1BD97B">today by {{ shipment }}</span>
              </div>
              <div v-if="shipment === 'JNE'">
                <span style="color: #1BD97B">delivered by {{ shipment }} for 2 days</span>
              </div>
              <div v-if="shipment === 'Personal Courier'">
                <span style="color: #1BD97B">delivered by {{ shipment }} for 1 day</span>
              </div>
            </div>
            <div style="margin: 10px 0;">
              <div v-if="payment">
                Payment Method
                <div>
                  <span style="color: #1BD97B">{{ payment }}</span>
                </div>
              </div>
            </div>
          </div>
          <div class="checkout-form__summary_items">
            <div class="checkout-form__summary_sub">
              <span>Cost of goods</span>
              <span style="font-weight: bold;">{{ costOfGoods }}</span>
            </div>
            <div v-if="isDropship" class="checkout-form__summary_sub">
              <span>Dropshipping Fee</span>
              <span style="font-weight: bold;">{{ dropFee }}</span>
            </div>
            <div v-if="step === 'paymentStep' || step === 'finishStep'" class="checkout-form__summary_sub">
              <span>{{ shipment }} Shipment</span>
              <span style="font-weight: bold;">{{ shipmentPrice }}</span>
            </div>
            <div class="checkout-form__summary_sub" style="font-size: 25px; margin-top: 20px;">
              <span class="text_color">Total</span>
              <span class="text_color">{{ total }}</span>
            </div>
            <div>
              <input v-if="step === 'deliveryStep' || step === null" type="button" class="custom-button" value="Continue to Payment" @click="nextStep('paymentStep')">
              <input v-else-if="step === 'paymentStep'" type="button" class="custom-button" :value="`Pay with ${shipment}`" @click="nextStep('finishStep')" :disabled="isPaymentForm">
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
      shipment: '',
      shipmentPrice: 0,
      deliveryCode: '',
      payment: '',
      costOfGoods: 500000,
      dropFee: 5900,
      total: 0,
      inputForm: [
        {
          type: 'email',
          placeholder: 'Email'
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
      ],
      value: {},
      isDropship: false,
      isPhoneValid: false,
      isDropshipPhoneValid: false,
      isDeliver: true,
      isPayment: false,
      isFinish: false
    }
  },
  mounted() {
    this.total = this.costOfGoods
    localStorage.setItem('step', 'deliveryStep')
  },
  computed: {
    isPaymentForm() {
      if (this.shipment !== '' && this.payment !== '') {
        return false
      } else {
        return true
      }
    }
  },
  methods: {
    nextStep(val) {
      if (val === 'deliveryStep') {
        this.isDeliver = true
      } else {
        this.isDeliver = false
      }
      if (val === 'paymentStep') {
        this.isPayment = true
      } else {
        this.isPayment = false
      }
      if (val === 'finishStep') {
        this.isFinish = true
      } else {
        this.isFinish = false
      }
      localStorage.setItem('data_input', JSON.stringify(this.value))
      const data = localStorage.getItem('data_input')
      const parseData = JSON.parse(data)
      if (this.isDropship) {
        if (
          parseData.email &&
          parseData.dropshipper_name &&
          parseData.phone_number &&
          parseData.dropshipper_phone_number &&
          parseData.address &&
          localStorage.getItem('isPhoneValid') &&
          localStorage.getItem('isPhoneDropValid')
        ) {
          this.step = val;
          localStorage.setItem('step', this.step);
          if (this.step === 'finishStep') {
            localStorage.setItem('step', 'deliveryStep');
            const randomCode = this.generateRandomCode();
            this.deliveryCode = randomCode;
          }
        } else {
          alert('Silahkan isi semua Field terlebih dahulu.');
        }
      } else {
        if (
          parseData.email &&
          parseData.phone_number &&
          parseData.address &&
          localStorage.getItem('isPhoneValid')
        ) {
          this.step = val;
          localStorage.setItem('step', this.step);
          if (this.step === 'finishStep') {
            localStorage.setItem('step', 'deliveryStep');
            const randomCode = this.generateRandomCode();
            this.deliveryCode = randomCode;
          }
        } else {
          alert('Silahkan isi semua field kecuali Dropshipper Name and Dropshipper Phone Number.');
        }
      }
    },
    generateRandomCode() {
      const characters = '23456789ABCDEFGHJKLMNPQRSTUVWXYZ';
      let result = '';

      for (let i = 0; i < 5; i++) {
        const randomIndex = Math.floor(Math.random() * characters.length);
        result += characters.charAt(randomIndex);
      }

      return result;
    },
    handleShipment(val, price) {
      this.shipment = val
      this.shipmentPrice = price
      this.total = this.dropFee + this.costOfGoods + this.shipmentPrice
    },
    handlePayment(val) {
      this.payment = val
    },
    handleForm(val) {
      this.value = val
    },
    handlePhoneNumber(val) {
      this.isPhoneValid = val
      localStorage.setItem('isPhoneValid', val)
    },
    handlePhoneNumberDropship(val) {
      this.isDropshipPhoneValid = val
      localStorage.setItem('isPhoneDropValid', val)
    },
    handleDrop(val) {
      if (val) {
        this.dropFee = 5900
      } else {
        this.dropFee = 0
      }
      this.total = this.dropFee + this.costOfGoods + this.shipmentPrice
      this.isDropship = val
    } 
  },
}
</script>
<style lang="stylus" scoped>
.checkout-form__back
  &:hover
    cursor pointer
.checkout-form
  margin 70px
  padding 40px
  background white
  border-radius 10px
  box-shadow 10px 20px 20px #979797
.checkout-form__section
  height 500px
  margin-top 30px
  display flex
  justify-content space-between
.checkout-form__left_details
  width 70%
.checkout-form__summary_details
  border-left 1px solid #FF8A00
  padding-left 10px
  width 30%
  display flex
  flex-direction column
  justify-content space-between
.checkout-form__summary_items
  display flex
  flex-direction column
.checkout-form__summary_sub
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