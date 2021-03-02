<template>
  <div class="symbol">
    <div class="points" v-if="points">
      <span class="one" v-for="p in points" :key="p"></span>
    </div>
    <div v-if="value != 20">
      <div class="five" v-for="f in fives" :key="f"></div>
    </div>
    <div v-if="value == 20" class="zero"></div>
  </div>
</template>

<script>
export default {
  name: "NumericSymbol",
  props: ['value'],
  data() {
    return {
      points: this.value % 5,
      fives: Math.floor(this.value / 5)
    }
  }
}
</script>

<style scoped lang="scss">
$symbol-color: gray;
.symbol {
  display: flex;
  flex-flow: column wrap;
  justify-content: flex-end;
  border-bottom: 1px solid $symbol-color;
  width: 50px;
  height: 48.3px;

  div {
    width: 40px;
    text-align: center;

  }

  .points {
    height: 18.3px;
  }

  .one {
    display: inline-block;
    background-color: $symbol-color;
    border-radius: 50%;
    height: 10px;
    width: 10px;
  }

  .five {
    background-color: $symbol-color;
    height: 5px;
    margin-bottom: 5px;
  }

  .zero {
    position: relative;
    border: 2px solid $symbol-color;
    border-radius: 50%;
    height: 10.5px;
    margin-bottom: 5px;

    &:before {
      content: '|||';
      position: absolute;
      border-radius: 50%;
      border: 2px solid $symbol-color;
      width: 100%;
      height: 6px;
      left: 0;
      top: 0;
      font-size: .5em;
      line-height: .5em;
    }
  }
}
</style>
