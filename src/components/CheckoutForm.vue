<template>
  <div>
    <div class="checkout_form">
      <StepperForm />
      <div class="back">
        Back to Cart
      </div>
      <div class="form_section">
        <div class="form_delivery">
          <div class="delivery_details">
            <span class="text_color" style="font-size: 35px;">Delivery details</span>
            <span> <input type="checkbox" name="isCheck" id="check"> Send as dropshipper</span>
          </div>
          <div class='some-page-wrapper'>
            <div class='row'>
              <div class='column'>
                <div class='blue-column'>
                  <input type="text" class="custom-input" placeholder="Name" />
                </div>
              </div>
              <div class='column'>
                <div class='green-column'>
                  <input type="text" class="custom-input" placeholder="Dropshipper Name" />
                </div>
              </div>
            </div>
            <div class='row'>
              <div class='column'>
                <div class='blue-column'>
                  <input type="number" class="custom-input" placeholder="Phone Number" />
                </div>
              </div>
              <div class='column'>
                <div class='green-column'>
                  <input type="text" class="custom-input" placeholder="Dropshipper Phone Number" />
                </div>
              </div>
            </div>
            <div class='row'>
              <div class='column'>
                <div class='blue-column'>
                  <input type="text" class="custom-input" placeholder="Delivery Address" />
                </div>
              </div>
            </div>
          </div>
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
              <input type="button" class="custom-button" value="Continue to Payment">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import StepperForm from '@/components/StepperForm.vue'
export default {
  name: 'CheckoutForm',
  components: {
    StepperForm,
  },
  data() {
    return {
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
  }
}
</script>
<style lang="stylus" scoped>
.checkout_form
  margin 90px
  padding 40px
  background white
  border-radius 10px
  box-shadow 10px 20px 20px #979797
.form_section
  height 500px
  margin-top 30px
  display flex
  justify-content space-between
.form_delivery
  diplay flex
  flex-direction column
  width 100%
  border-right 1px solid #FF8A00
  margin-right 10px
.delivery_details
  width 90%
  display flex
  justify-content space-between
  margin-bottom 20px
.summary_details
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
.form_details
  width 100%
  background blue
  display flex
  flex-direction column
.custom-input
  margin-bottom 10px
  border 1px solid #ccc
  padding 15px
  font-size 20px
  color #333
  min-width 400px
  height 60px
  &:focus
    outline none
    border-color #ccc
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