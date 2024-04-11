<template>
  <div>
    <div style="display: flex; justify-content: center;">
      <div style="display: flex; gap: 20px; background-color: #FFFAE6; color: black; transform: translateY(-60px); padding: 10px 25px; border-radius: 100px;">
        <div style="display: flex; color: #FF8A00; align-items: center; gap: 20px;">
          <div style="background-color: #FF8A00; border-radius: 100%; width: 20px; padding: 10px; color: #FFFAE6; text-align: center;">
            1
          </div>
          Delivery
          <div>></div>
        </div>
        <div style="display: flex; color: #FF8A00; align-items: center; gap: 20px;">
          <div style="background-color: #FF8A00; border-radius: 100%; width: 20px; padding: 10px; color: #FFFAE6; text-align: center;">
            2
          </div>
          Payment
          <div>></div>
        </div>
        <div style="display: flex; color: #FF8A00; align-items: center; gap: 20px;">
          <div style="background-color: #FF8A00; border-radius: 100%; width: 20px; padding: 10px; color: #FFFAE6; text-align: center;">
            3
          </div>
          Finish
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'StepperForm'
}
</script>