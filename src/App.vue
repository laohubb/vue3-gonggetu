<script setup>
import Palace from './components/Place.vue'
</script>

<template>
  <div class="box">
    <h2>志存印象</h2>
    <p>“存志”品牌始于1996年，语出诸葛亮《诫外生书》——“志当存高远”。希冀以“存志”二字，勉励少年壮志，养浩然之气，树远大</p>
    <p>理想，植家国情怀，拓国际视野。希望莘莘学子在此道路上，孜孜进取，追求卓越，为人类更美好的共同命运领航。</p>
    <Palace />
  </div>
</template>

<style scoped>
.box {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;

}

h2 {
  color: #3b4b6b;
  margin: 0 auto;
  padding: 30px;
}
</style>
