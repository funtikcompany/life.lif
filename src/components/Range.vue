<template>
  <div class="progress-bar">
    <progress :max="maxProgress" :value="progress"></progress>
  </div>
</template>

<script>
export default {
  props: {
    progress: {
      type: Number,
      required: true,
    },
    maxProgress: {
      type: Number,
      required: true,
    },
  },
};
</script>
