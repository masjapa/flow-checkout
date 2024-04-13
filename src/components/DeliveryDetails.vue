<template>
  <div class="form-delivery">
    <div class="form-delivery__delivery_details">
      <span class="text_color" style="font-size: 35px;">Delivery details</span>
      <span> <input type="checkbox" name="isCheck" id="check" v-model="isDropshipChecked" @change="isDropToggle"> Send as dropshipper</span>
    </div>
    <div>
      <div class='form-delivery__row'>
        <div class='form-delivery__column'>
          <div class='form-delivery__left-column'>
            <input type="email" class="custom-input" placeholder="Email" @input="emitData" v-model="formDelivery.email" />
          </div>
        </div>
        <div class='form-delivery__column'>
          <div class='form-delivery__right-column'>
            <input type="text" class="custom-input" placeholder="Dropshipper Name" @input="emitData" :disabled="!isDropshipChecked" v-model="formDelivery.dropshipper_name" />
          </div>
        </div>
      </div>
      <div class='form-delivery__row'>
        <div class='form-delivery__column'>
          <div class='form-delivery__left-column'>
            <input type="tel" class="custom-input" placeholder="Phone Number" pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}" required @input="validatePhoneNumber" v-model="formDelivery.phone_number" :class="{ 'valid': isPhoneNumberValid && formDelivery.phone_number !== '', 'invalid': !isPhoneNumberValid && formDelivery.phone_number !== '' }" />
          </div>
        </div>
        <div class='form-delivery__column'>
          <div class='form-delivery__right-column'>
            <input type="tel" class="custom-input" placeholder="Dropshipper Phone Number" pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}" required @input="validateDropshipperPhoneNumber" :disabled="!isDropshipChecked" v-model="formDelivery.dropshipper_phone_number" :class="{ 'valid': isDropshipperPhoneNumberValid && formDelivery.dropshipper_phone_number !== '', 'invalid': !isDropshipperPhoneNumberValid && formDelivery.dropshipper_phone_number !== '' }" />
          </div>
        </div>
      </div>
      <div class='form-delivery__row'>
        <div class='form-delivery__column'>
          <div class='form-delivery__left-column'>
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
        email: '',
        dropshipper_name: '',
        phone_number: '',
        dropshipper_phone_number: '',
        address: ''
      },
      isDropshipChecked: false,
      isPhoneNumberValid: false,
      isDropshipperPhoneNumberValid: false
    }
  },
  methods: {
    emitData() {
      this.$emit('input', this.formDelivery);
    },
    isDropToggle() {
      this.$emit('isDrop', this.isDropshipChecked);
    },
    validatePhoneNumber() {
      const phoneNumberPattern = /^[0-9,+() -]{6,20}$/;
      this.isPhoneNumberValid = phoneNumberPattern.test(this.formDelivery.phone_number);
      this.$emit('isPhoneValid', this.isPhoneNumberValid)
    },
    validateDropshipperPhoneNumber() {
      if (this.isDropshipChecked) {
        const dropshipperPhoneNumberPattern = /^[0-9,+() -]{6,20}$/;
        this.isDropshipperPhoneNumberValid = dropshipperPhoneNumberPattern.test(this.formDelivery.dropshipper_phone_number);
      } else {
        this.isDropshipperPhoneNumberValid = true;
      }
      this.$emit('isPhoneDropshipValid', this.isDropshipperPhoneNumberValid)
    }
  }
}
</script>

<style lang="stylus" scoped>
.form_delivery
  display: flex
  flex-direction: column
.form-delivery__delivery_details
  width: 90%
  display: flex
  justify-content: space-between
  margin-bottom: 20px
.text_color
  color: #FF8A00
  font-weight: bold
.custom-input
  margin-bottom: 10px
  border: 1px solid #ccc
  padding: 15px
  font-size: 20px
  color: #333
  min-width: 350px
  height: 60px
  &:focus
    outline: none
    border-color: #ccc
.form-delivery__row
  display: flex
  flex-direction: form-delivery__row
  flex-wrap: wrap
  width: 100%
.form-delivery__column
  display: flex
  flex-direction: column
  flex-basis: 100%
  flex: 1

.valid
  border 1px solid green
.invalid
  border 1px solid red

.error-msg
  color: red
  font-size: 14px
</style>
