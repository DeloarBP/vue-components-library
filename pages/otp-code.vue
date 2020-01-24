<template>
  <div>
    <otp-code-input
      :num-inputs="4"
      :should-auto-focus="true"
      :is-input-num="true"
      @on-complete="handleOnComplete"
      input-classes="otp-input"
      separator="-"
    ></otp-code-input>
  </div>
</template>
<script>
import OtpCodeInput from '~/components/otpCode/Otp-Code'
export default {
  name: 'OtpCode',
  components: { OtpCodeInput },
  methods: {
    handleOnComplete(value) {
      //   console.log('OTP: ', value)
    }
  }
}
</script>

<style>
/*
.otp-input {
  width: 40px;
  height: 40px;
  padding: 5px;
  margin: 0 10px;
  font-size: 20px;
  border-radius: 4px;
  border: 1px solid rgba(0, 0, 0, 0.3);
  textalign: 'center';
  &.error {
    border: 1px solid red !important;
  }
}
*/
</style>
