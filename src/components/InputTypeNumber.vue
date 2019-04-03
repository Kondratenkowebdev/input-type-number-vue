<template>
  <div
      :class="wrapperClass"
      class="b-input-wrapper">
      <label
          v-if="title"
          class="b-input-title"
          :for="id">{{ title }}</label>
      <div class="b-input-inner">
          <input
              v-model="inputValue"
              type='tel'
              :name="name"
              :id="randomId"
              :placeholder="placeholder"
              :disabled="isDisabled"
              @keypress="onKeypress"
              @paste="onPaste"
              @blur="onBlur"/>

          <div class='b-input-arrows-wrapper'>
              <span class='b-input-arrow b-input-increase'
                    @click='changeValueIncrease'>
                    &uarr;
              </span>
              <span class='b-input-arrow b-input-decrease'
                    @click='changeValueDecrease'>
                  &darr;
              </span>
          </div>
      </div>
      <div v-if='error'
           class='b-input-error'>
          {{ error }}
      </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'InputTypeNumber',
   data() {
       return {
           value: 0,
           currentValue: '',
       };
  },
  props: {
    startValue: {
      type: Number,
    },
    name: {
      type: String,
      required: true,
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    addFocus: {
      type: Boolean,
    },
    title: {
      type: String,
    },
    wrapperClass: {
      type: String,
    },
    id: {
      type: String,
    },
    placeholder: {
      type: String,
    },
    error: {
      type: String,
    },
    step: {
      type: Number,
      default: 1,
    },
  },
  computed: {
      randomId(): string  {
          return this.id || `input-${this._uid}`;
      },
      inputValue: {
          get(): string  {
              return this.currentValue;
          },
          set(value: string) {
              this.currentValue = value;
              this.$forceUpdate();
          },
      },
  },
  methods: {
      onKeypress(event: any) {
          if (!this.isAvailableSymbol(event.charCode)) {
              event.preventDefault();
          }
      },
      onBlur() {
          this.currentValue = this.processingValue(this.currentValue);
      },
      onPaste(value: any) {
          if (isNaN(parseFloat(value))) {
              this.currentValue = this.processingValue(this.currentValue);
          }
      },
      processingValue(value: string): string {
          return parseFloat(value).toFixed(2);
      },
      isAvailableSymbol(charCode: number): boolean {
          const value = String.fromCharCode(charCode);
          const dot = '.';
          if (value === dot && !this.currentValue.includes(dot)) {
              return true;
          }
          return Number.isInteger(+value);
      },
      changeValueIncrease() {
          this.currentValue = this.processingValue(String(+this.currentValue + this.step));
      },
      changeValueDecrease() {
          const decreaseValue = +this.currentValue - this.step;
          const value = decreaseValue < 0 ? +this.currentValue : decreaseValue;
          this.currentValue = this.processingValue(String(value));
      },
  },
  created() {
      this.currentValue = this.processingValue(String(Math.abs(this.startValue)));
  },
});
</script>

<style lang="sass">
.b-input-wrapper
  display: flex
  flex-direction: column
  width: 100%

.b-input-title
  font-size: 14px
  display: flex

.b-input-inner
  width: 100%
  display: flex

input
  outline: none
  box-shadow: none
  border-radius: 0
  width: 100%
  display: block
  padding: 8px

input[type=tel]
  -moz-appearance: textfield
  appearance: textfield
  margin: 0

.b-input-arrows-wrapper
    display: flex
    flex-direction: row
    padding: 0 5px

.b-input-arrow
    display: flex
    flex: 1 0
    padding: 4px
    font-size: 13px
    cursor: pointer
    user-select: none

    &:hover
        color: green
    
.b-input-error
    color: red
    display: flex
    font-size: 14px
</style>
