<template>
  <div class="container">

      <HeadBlock label="Matte" :colors="combineColors('#444')"/>
      <ColorBlock type="Dark" :colors="combineColors(darkColorMatte)"/>
      <ColorBlock type="Shadow" :colors="combineColors(shadowColorMatte)"/>
      <ColorBlock type="Base" :colors="combineColors(baseColor)" class="span3" stretch/>
      <ColorBlock type="Highlight" :colors="combineColors(highlightColorMatte)"/>
      <ColorBlock type="Glare" :colors="combineColors(glareColorMatte)"/>

      <HeadBlock label="Glossy" :colors="combineColors('#aaa')"/>
      <ColorBlock type="" :colors="combineColors(darkColorGlossy)"/>
      <ColorBlock type="" :colors="combineColors(shadowColorGlossy)"/>
      <!-- <ColorBlock type="" :colors="combineColors(baseColor)" hide/> -->
      <ColorBlock type="" :colors="combineColors(highlightColorGlossy)"/>
      <ColorBlock type="" :colors="combineColors(glareColorGlossy)"/>

      <HeadBlock label="Metallic" :colors="combineColors('#777')"/>
      <ColorBlock type="" :colors="combineColors(darkColorMetallic)"/>
      <ColorBlock type="" :colors="combineColors(shadowColorMetallic)"/>
      <!-- <ColorBlock type="" :colors="combineColors(baseColor)"/> -->
      <ColorBlock type="" :colors="combineColors(highlightColorMetallic)"/>
      <ColorBlock type="" :colors="combineColors(glareColorMetallic)"/>
    </div>

      <div class="control">
        <label for="baseColor">Base Color&nbsp;</label>
        <input id="baseColor" type="color" v-model="baseColor" @input="transformColors"/>
      </div>

</template>

<script>
import Color from 'color'
import ColorBlock from './components/ColorBlock.vue'
import HeadBlock from './components/HeadBlock.vue'

export default {
  components: {
    ColorBlock, HeadBlock,
    HeadBlock
},
  created(){
    this.transformColors()
  },
  mounted() {
    this.transformColors()
  },
  data() {
    return {
      baseColor: '#C0A8A0', // Default color
      highlightColorMatte: '',
      glareColorMatte: '',
      shadowColorMatte: '',
      darkColorMatte: '',
      highlightColorGlossy: '',
      glareColorGlossy: '',
      shadowColorGlossy: '',
      darkColorGlossy: '',
      highlightColorMetallic: '',
      glareColorMetallic: '',
      shadowColorMetallic: '',
      darkColorMetallic: '',
      materialType: 'matte'
    };
  },
  methods: {
  transformColors() {
    const base = Color(this.baseColor);
      this.highlightColorMatte = this.blendScreen(base, Color('#494840'))
      this.glareColorMatte = this.blendScreen(base, Color('#a98'))
      this.shadowColorMatte = this.blendDarken(base, Color('#abc'));
      this.darkColorMatte = this.blendDarken(base, Color('#569'))
      this.highlightColorGlossy = this.blendScreen(base, Color('#605550'))
      this.glareColorGlossy = this.blendScreen(base, Color('#edd'))
      this.shadowColorGlossy = this.blendDarken(base, Color('#c6d2ec'));
      this.darkColorGlossy = this.blendDarken(base, Color('#568'))
      this.highlightColorMetallic = this.blendScreen(base, Color('#889'))
      this.glareColorMetallic = this.blendScreen(base, Color('#ccc'))
      this.shadowColorMetallic = this.blendDarken(base, Color('#889'));
      this.darkColorMetallic = this.blendDarken(base, Color('#344'))
  },
  combineColors(color) {
    let arr = [
      color,
      Color(color).isDark() ? '#fff' : '#000',
      Color(color).isDark() ? '#000' : '#fff'
    ]
    return arr
  },
  normalizeRGB(rgb) {
    return [rgb.red() / 255, rgb.green() / 255, rgb.blue() / 255];
  },
  mapRGB(rgb) {
    return [rgb[0] * 255, rgb[1] * 255, rgb[2] * 255];
  },
  blendDarken(A, B) {
    let a = this.normalizeRGB(A);
    let b = this.normalizeRGB(B);
    let c = [a[0] * b[0], a[1] * b[1], a[2] * b[2]];
    c = this.mapRGB(c);
    return Color(c).hex();
  },
  blendScreen(A, B) {
    let a = this.normalizeRGB(A);
    let b = this.normalizeRGB(B);
    let c = [1 - (1 - a[0]) * (1 - b[0]), 1 - (1 - a[1]) * (1 - b[1]), 1 - (1 - a[2]) * (1 - b[2])];
    c = this.mapRGB(c);
    return Color(c).hex();
  }
}

}
</script>

<style>
body {
  background: linear-gradient(0deg, #444, #888);
}
label {
  margin: 0 0.5em 0 0.2em;
}
#app {
  grid-template-columns: 1fr 2fr 1fr;
}
#baseColor {
  border-radius: 0;
  /* border: 2px solid rgba(0, 0, 0, 0); */
  border: none;
  background: none;
  cursor: pointer;
  width: 9em;
  height: 5em;
  padding: 0;
  margin: 0;
  box-shadow: rgba(0, 0, 0, 0.3) 6px 6px 8px;
}
#baseColor:hover {
  /* border: 2px solid red; */
  filter: brightness(1.2);
}
#baseColor:active {
  filter: brightness(0.8);
}
label {
  user-select: none;
}
label:hover {
  cursor: pointer;
  filter: brightness(1.75);
}
label:active {
  filter: brightness(0.75);
}
.container {
  grid-column: 2/3;
  display: grid;
  grid-template-columns: 0fr 2fr 2fr 2fr 2fr 2fr;
  box-shadow: rgba(0, 0, 0, 0.3) 2px 2px 8px;
}
.blocks {
  display: flex;
  flex-direction: row;
}
.control {
  display: flex;
  flex-direction: row;
  align-items: center;
  align-content: stretch;
  grid-column: 2/3;
  justify-content: center;
  text-transform: uppercase;
  font-weight: 600;
  font-family: monospace;
  color: #fff;
  text-shadow: rgba(0, 0, 0, 1) 2px 2px 6px;
  margin-top: 1em;
}
.span3 {
  grid-column: 4;
  grid-row: 1 / 4;
}
</style>