<script setup lang="ts">
import { useReplicant } from 'nodecg-vue-composable';
import { computed, Ref, ref } from 'vue';
import type {
  RunDataActiveRunSurrounding,
  RunDataArray,
} from '@GsRR2024-layouts/types/schemas/speedcontrol';
import UpnextSchedule from './upNextSchedule.vue';
import OndeckSchedule from './OndeckSchedule.vue'
import * as util from '../../util/format';

const runDataArray = useReplicant<RunDataArray>('runDataArray', 'nodecg-speedcontrol');

const runDataActiveRunSurrounding = useReplicant<RunDataActiveRunSurrounding>(
  'runDataActiveRunSurrounding',
  'nodecg-speedcontrol'
);

const speedcontrolActiveRunIndex = computed(() => {
  const activeRunIndex = runDataArray?.data?.findIndex(
    (runData) => runData.id === runDataActiveRunSurrounding?.data?.current
  );
  return activeRunIndex;
});

const upcomingRuns = computed(() => {
  const index = speedcontrolActiveRunIndex.value || 0;
  return runDataArray?.data?.slice(index, index + 3);
});

const upnextRun = computed(() => upcomingRuns?.value?.[0]);

const ondeckRuns = computed(() => upcomingRuns.value?.slice(1));

const upcomingStartIn = computed(() => {
  if (!upcomingRuns.value || !upcomingRuns.value[1]) {
    return [];
  }

  const startInArray = [];
  const secondRunStartIn =
    (upcomingRuns.value[0].estimateS || 0) + (upcomingRuns.value[1].setupTimeS || 0);
  startInArray.push(util.formatSecondsToStartInTime(secondRunStartIn));

  if (!upcomingRuns.value[2]) {
    return startInArray;
  }
  const thirdRunStartIn =
    secondRunStartIn +
    (upcomingRuns.value[1].estimateS || 0) +
    (upcomingRuns.value[2].setupTimeS || 0);
  startInArray.push(util.formatSecondsToStartInTime(thirdRunStartIn));
  return startInArray;
});

let isShow: Ref<number> = ref(0);
setInterval(() => {
  switch (isShow.value) {
    case 0:
      isShow.value++;
      break;
    case 1:
      isShow.value++;
      break;
    case 2:
      isShow.value = 0;
  }
  }, 30000);
  //5000 = 5秒
</script>

<template>
  <!--<div id="next">NEXT</div>-->
  <div class="mokuji">
    <UpnextSchedule :run-data="upnextRun" />
    <OndeckSchedule
      v-for="(run, index) in ondeckRuns"
      :key="run.id"
      :class="`next${index + 2}`"
      :run-data="run"
      :upcoming-start-in="upcomingStartIn[index]"
      :show-category-runner="index < 2"/>
  </div>
  <div class="marquee">
    <div v-show="isShow === 0" class="marquee-inner">
      <span>SNSハッシュタグ </span>
      <span style="color:Red">＃ガストRTAリレー</span>
      <span> で走者に感想を送ろう！</span>
    </div>
    <div v-show="isShow === 1" class="marquee-inner">
      <span>イベントスケジュールが知りたい？ </span>
      <span style="color:Red">!schedule</span>
      <span> をチャットに送信！</span>
    </div>
    <div v-show="isShow === 2" class="marquee-inner">
      <span>待機画面の素敵なBGMはこちら！ RYU ITO - </span>
      <span style="color:Red">https://ryu110.com/</span>
    </div>
  </div>
</template>
