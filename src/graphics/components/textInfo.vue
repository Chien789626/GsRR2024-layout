<script setup lang="ts">
</script>

<template>
  <div class="marquee">
    <div class="loop wspace">
      <span>SNSハッシュタグ </span>
      <span style="color:Red">＃ガストRTAリレー</span>
      <span> で走者に感想を送ろう！</span>
    </div>
    <div class="loop loop2">
      <span>イベントスケジュールが知りたい？ </span>
      <span style="color:Red">!schedule</span>
      <span> をチャットに送信！</span>
    </div>
  </div>
</template>

<style>
.marquee {
  position: absolute;
  overflow: hidden;
  width: 1300px;
  height: 50px;
  bottom: 0;
  font-size: 38px;
  font-family: 'KomorebiGothic';
  /* border: 1px solid black; */
}
.loop {
  width: 100%;
  position: absolute;
  text-align: center;
  bottom: 5px;
  animation: loop 120s linear infinite;
  /* border: 1px solid red; */
}

.loop2 {
  position: absolute;
  width: 100%;
  animation: loop 120s -60s linear infinite;
  /* border: 1px solid rgb(0, 68, 255); */
}

.wspace{
  padding-right: 0px;
}

@keyframes loop {
  0%{ transform: translateX(100%); }
  100%{ transform: translateX(-100%); }
}
</style>