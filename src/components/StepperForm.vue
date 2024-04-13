<template>
  <div class="stepper-form">
    <div class="step">
      <div :class="{ 'step__item': true, 'active': deliveryStep }">
        <div class="step__circle">1</div>
        Delivery
      </div>
      <div :class="{ 'step__item': true, 'active': paymentStep }">
        <div class="step__circle">2</div>
        Payment
      </div>
      <div :class="{ 'step__item': true, 'active': finishStep }">
        <div class="step__circle">3</div>
        Finish
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StepperForm',
  props: {
    deliveryStep: {
      type: Boolean,
      default: false
    },
    paymentStep: {
      type: Boolean,
      default: false
    },
    finishStep: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="stylus" scoped>
.stepper-form
  display: flex
  justify-content: center

.step
  display: flex
  gap: 20px
  background-color: #FFFAE6
  color: black
  transform: translateY(-60px)
  padding: 10px 25px
  border-radius: 100px

.step__item
  display: flex
  color: #FF8A00
  align-items: center
  gap: 20px

.step__circle
  background-color: #FF8A00
  border-radius: 100%
  width: 20px
  padding: 10px
  color: #FFFAE6
  text-align: center

.step__item.active .step__circle
  background-color: #FF8A00

.step__item:not(.active) .step__circle
  background-color: #f7ba72
</style>
