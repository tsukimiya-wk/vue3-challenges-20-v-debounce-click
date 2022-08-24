<script setup lang="ts">
/**
 * Implement the custom directive
 * Make sure the `onClick` method only gets triggered once when clicked many times quickly
 * And you also need to support the debounce delay time option. e.g `v-debounce-click:ms`
 *
 */

const debounce = (fn, delay = 1000) => {
  let timer;

  return function (...args) {
    if (timer) {
      return;
    }
    fn.apply(this, args);
    timer = setTimeout(() => {
      clearTimeout(timer);
      timer = null;
    }, delay);
  };
};

const VDebounceClick = {
  mounted: (el, binding) => {
    el.addEventListener('click', debounce(binding.value, binding.arg));
  },
};

function onClick() {
  console.log('Only triggered once when clicked many times quickly');
}
</script>

<template>
  <button v-debounce-click:200="onClick">Click on it many times quickly</button>
</template>
