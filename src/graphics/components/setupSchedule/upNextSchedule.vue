<script setup lang="ts">
import { computed } from 'vue';
import type { RunData } from '@GsRR2024-layouts/types/schemas/speedcontrol';

interface Props {
  runData?: RunData;
}

const props = defineProps<Props>();

const runners = computed(() => {
  if (!props.runData) {
    return '';
  }
  // eslint-disable-next-line max-len
  return props.runData.teams
    .flatMap((team) => team.players.flatMap((player) => player.name))
    .join(', ');
});
</script>

<template>
  <div class="next1">
    <div class="title">
      {{ props.runData?.game }}
    </div>
    <div v-if="props.runData?.category != '-'" class="category_runner">
      <span class="category">{{ props.runData?.category }}</span>
      <span class="est"> / {{ props.runData?.estimate }}</span>
      <div class="runner">走者  {{ runners }}</div>
    </div>
  </div>
</template>
