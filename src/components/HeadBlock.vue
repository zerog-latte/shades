<script setup>
const props = defineProps({
  colors: {
    type: Array,
    required: true
  },
  label: {
    type: String,
    required: false
  }
})
</script>

<template>
<div class="box" @click="copyToClipboard">
  <div class="color label">{{ label }}</div>
</div>
</template>

<style scoped>
.box {
  /* height: 9em; */
  
}
.box:hover {
  filter: brightness(1.1);
}
.box:active {
  filter: brightness(0.9);
}
.color {
  background-color: v-bind(colors[0]);
}
.label {
  align-self: stretch;
  height: 12em;
  text-align: center;
  text-transform: lowercase;
  writing-mode: vertical-lr;
  text-orientation: upright;
  font-variant: small-caps;
  padding-top: 0.7em;
  user-select: none;
  color: v-bind(colors[1]);
  text-shadow: v-bind(colors[2]) 0px 0px 6px;
}
</style>
