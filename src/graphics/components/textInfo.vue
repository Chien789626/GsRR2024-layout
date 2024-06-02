<script setup lang="ts">
</script>

<template>
  <div class="marquee">
    <p class="loop">これは1つ目のメッセージです。これは1つ目のメッセージです。</p>
    <p class="loop loop2">これは2つ目のメッセージです。これは2つ目のメッセージです。</p>
  </div>
</template>

<style>
.marquee {
  position: absolute;
  overflow: hidden;
  width: 1530px;
  height: 50px;
  bottom: 0;
  font-size: 34px;
  font-family: 'KomorebiGothic';
  border: 1px solid black;
}
.loop {
  width: 100%;
  position: absolute;
  bottom: 5px;
  animation: loop 10s linear infinite;
  border: 1px solid red;
}

.loop2 {
  position: absolute;
  animation: loop 10s -5s linear infinite;
}

@keyframes loop {
  0%{ transform: translateX(100%); }
  100%{ transform: translateX(-100%); }
}
</style>