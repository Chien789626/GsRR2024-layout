<script setup lang="ts">
import { computed } from 'vue';
import type { RunData } from '@GsRR2024-layouts/types/schemas/speedcontrol';

interface Props {
  runData?: RunData,
  upcomingStartIn?: string
  showCategoryRunner?: boolean
}

const props = defineProps<Props>();

const runners = computed(() => {
  if (!props.runData) {
    return '';
  }
  // eslint-disable-next-line max-len
  return props.runData.teams.flatMap((team) => team.players.flatMap((player) => player.name)).join(', ');
});

</script>

<template>
  <div>
    <div class="title">
      {{ runData?.game }}
    </div>
    <div class="category_runner" v-if="props.showCategoryRunner">
      <span class="category">{{ runData?.category }}</span>
      <span class="est"> {{ runData?.estimate }}</span>
      <p class="runner">{{ runners }}</p>
    </div>
  </div>
</template>
