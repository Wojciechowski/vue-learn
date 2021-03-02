<template>
  <div class="maya">
    <h1>Maya calendar long count</h1>
    <ul class="kin">
      <li v-for="kin in 20" :key="kin">
        <span v-if="kin != 20">{{kin}}</span><span v-if="kin == 20">0</span> = <span> <numeric-symbol :value="kin"></numeric-symbol></span>
      </li>
    </ul>
  </div>
</template>

<script>
import NumericSymbol from "@/components/NumericSymbol";

export default {
  name: "LongCount",
  components: {NumericSymbol}
}
</script>

<style scoped lang="scss">
.kin{
  span{
    display: inline-block;
  }
}
</style>
