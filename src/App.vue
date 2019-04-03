<template>
  <div>
    <InputTypeNumber
      :startValue='345.3'
      name='productCost'
      title='Product Cost'
      :step='5'
      wrapperClass='b-some-dynamic-class'>
    </InputTypeNumber>

    <InputTypeNumber
      :startValue='11'
      name='anotherCost'
      title='Another Cost'
      wrapperClass='b-some-dynamic-class'>
    </InputTypeNumber>

    <InputTypeNumber
      :startValue='-30'
      name='anotherCost2'
      title='Another Cost negative'
      :step='0.25'
      wrapperClass='b-some-dynamic-class'>
    </InputTypeNumber>

    <InputTypeNumber
      :startValue='444'
      name='anotherCost2'
      title='Another Cost negative'
      error='some server error'
      :step='10'
      wrapperClass='b-some-dynamic-class'>
    </InputTypeNumber>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import InputTypeNumber from './components/InputTypeNumber.vue';

export default Vue.extend({
  name: 'app',
  components: {
    InputTypeNumber,
  },
});
</script>

<style lang='sass'>
body
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50

.b-some-dynamic-class
  width: 200px

  &:not(:first-of-type)
    margin-top: 10px
</style>
