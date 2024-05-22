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
    <div class="category_runner">
      <span v-if="props.runData?.category != '-'" class="category">{{ props.runData?.category }} /</span>
      <span class="est">{{ props.runData?.estimate }}</span>
      <span class="runner">{{ runners }}</span>
    </div>
  </div>
</template>
