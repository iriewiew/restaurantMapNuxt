<template>
  <meter class="average-rating" min="0" max="5" :value="value"></meter>
</template>

<script setup>
defineProps(["value"]);
</script>

<style lang="scss" scoped>
$meter-background: url('data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"%3E%3Ctext font-size="100" x="50%" y="60%" dominant-baseline="middle" text-anchor="middle" stroke-linejoin="round" fill="white" stroke="darkorange" stroke-width="4"%3E★%3C/text%3E%3C/svg%3E')
  0 / auto 100%;
$meterbar: url('data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"%3E%3Ctext font-size="100" x="50%" y="60%" dominant-baseline="middle" text-anchor="middle" stroke-linejoin="round" fill="gold" stroke="darkorange" stroke-width="4"%3E★%3C/text%3E%3C/svg%3E')
  0 / auto 100%;

meter {
  $meter-height: 1em;

  background: $meter-background;
  height: $meter-height;
  width: auto;
  aspect-ratio: 5 / 1;
}

meter::-webkit-meter-bar {
  background: $meter-background;
  border: none;
}

/* firefox styling for the bar (filled stars) */
meter:-moz-meter-optimum::-moz-meter-bar,
meter:-moz-meter-sub-optimum::-moz-meter-bar,
meter:-moz-meter-sub-sub-optimum::-moz-meter-bar {
  background: $meterbar;
}

/* webkit styling for the bar (filled stars) */
meter::-webkit-meter-optimum-value,
meter::-webkit-meter-suboptimum-value,
meter::-webkit-meter-even-less-good-value {
  background: $meterbar;
}

meter::-webkit-meter-inner-element {
  display: block;
}
</style>
