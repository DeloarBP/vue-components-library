<template>
  <div style="display: flex; align-items: center;">
    <input
      ref="input"
      :class="inputClasses"
      :type="isInputNum ? 'number' : 'tel'"
      v-model="model"
      @input="handleOnChange"
      @keydown="handleOnKeyDown"
      @paste="handleOnPaste"
      @focus="handleOnFocus"
      @blur="handleOnBlur"
      min="0"
      max="9"
    />
    <span v-if="!isLastChild && separator">
      <span v-html="separator"></span>
    </span>
  </div>
</template>
<script>
export default {
  name: 'SingleInput',
  props: {
    value: {
      type: String,
      default: '',
      required: false
    },
    separator: {
      type: String,
      default: '',
      required: false
    },
    focus: {
      type: Boolean
    },
    inputClasses: {
      type: String,
      default: '',
      required: false
    },
    shouldAutoFocus: {
      type: Boolean
    },
    isInputNum: {
      type: Boolean
    },
    isLastChild: {
      type: Boolean
    }
  },
  data() {
    return {
      model: this.value || ''
    }
  },
  watch: {
    value(newValue, oldValue) {
      if (newValue !== oldValue) {
        this.model = newValue
      }
    },
    // whenever question changes, this function will run
    focus(newFocusValue, oldFocusValue) {
      // Check if focusedInput changed
      // Prevent calling function if input already in focus
      if (oldFocusValue !== newFocusValue && this.$refs.input && this.focus) {
        this.$refs.input.focus()
        this.$refs.input.select()
      }
    }
  },
  mounted() {
    if (this.$refs.input && this.focus && this.shouldAutoFocus) {
      this.$refs.input.focus()
    }
  },
  methods: {
    handleOnChange() {
      if (this.model.length > 1) {
        this.model = this.model.slice(0, 1)
      }
      return this.$emit('on-change', this.model)
    },
    handleOnKeyDown(event) {
      return this.$emit('on-keydown', event)
    },
    handleOnPaste(event) {
      return this.$emit('on-paste', event)
    },
    handleOnFocus() {
      this.$refs.input.select()
      return this.$emit('on-focus')
    },
    handleOnBlur() {
      return this.$emit('on-blur')
    }
  }
}
</script>
