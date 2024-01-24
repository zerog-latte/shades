<script setup>
function copyToClipboard() {
  navigator.clipboard.writeText(props.color);
}

const props = defineProps({
  colors: {
    type: Array,
    required: true
  },
  type: {
    type: String,
    required: false
  },
  hide: {
    type: Boolean,
    required: false,
  },
  stretch: {
    type: Boolean,
    required: false
  }
})
let height = props.stretch ? '30em' : '6em';
</script>

<template>
<div class="box" @click="copyToClipboard">
  <div class="color label">{{ type }}</div>
  <div class="color sample"></div>
  <div class="color label hex">{{ hide ? '' : `${colors[0]}` }}</div>
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
.sample {
  width: 7em;
  height: v-bind(height);
}
.color {
  background-color: v-bind(colors[0]);
}
.label {
  height: 3em;
  text-align: center;
  text-transform: lowercase;
  font-variant: small-caps;
  padding-top: 0.7em;
  user-select: none;
  color: v-bind(colors[1]);
  text-shadow: v-bind(colors[2]) 0px 0px 6px;
}
.hex {
  text-transform: uppercase;
  font-weight: 600;
  font-family: monospace;
  padding-bottom: 1em;
}
</style>
