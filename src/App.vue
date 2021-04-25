<template>
  <div id="app" class="app">
    <div class="nauseda-container">
      <img
        :src="currentGlasses"
        class="glasses"
        :class="`glasses--${currentGlassesIndex + 1}`"
      />
      <img
        :src="currentHair"
        class="hair"
        :class="`hair--${currentHairIndex + 1}`"
      />
      <div class="sunglass-control-right" @click="prevGlasses">
        <img src="@/assets/play.svg" class="sunglass-control__control" />
      </div>
      <div class="sunglass-control-left" @click="nextGlasses">
        <img src="@/assets/play.svg" class="sunglass-control__control" />
      </div>
      <div class="hair-control-right" @click="prevHair">
        <img src="@/assets/play.svg" class="sunglass-control__control" />
      </div>
      <div class="hair-control-left" @click="nextHair">
        <img src="@/assets/play.svg" class="sunglass-control__control" />
      </div>
      <img src="@/assets/nauseda.png" class="nauseda" />
    </div>
    <audio src="@/assets/himnas.mp3" autoplay controls/>
  </div>
</template>

<script>
import akiniai1 from "@/assets/akiniai-1.svg";
import akiniai2 from "@/assets/akiniai-2.svg";
import akiniai3 from "@/assets/akiniai-3.svg";
import akiniai4 from "@/assets/akiniai-4.svg";
import hair1 from "@/assets/hair-1.svg";
import hair2 from "@/assets/hair-2.svg";
import hair3 from "@/assets/hair-3.svg";

const GLASSES = [akiniai1, akiniai2, akiniai3, akiniai4];
const HAIR = [hair1, hair2, hair3];

export const preloadImages = (images) =>
  images.map((image) => {
    const newImage = new Image();

    newImage.src = image;

    return newImage;
  });

export default {
  data() {
    return {
      currentGlassesIndex: 0,
      currentHairIndex: 0,
    };
  },
  computed: {
    currentGlasses() {
      return GLASSES[this.currentGlassesIndex];
    },
    currentHair() {
      return HAIR[this.currentHairIndex];
    },
  },
  mounted() {
    preloadImages([...GLASSES, ...HAIR]);
  },
  methods: {
    nextGlasses() {
      if (this.currentGlassesIndex + 2 > GLASSES.length) {
        this.currentGlassesIndex = 0;
        return;
      }

      this.currentGlassesIndex = this.currentGlassesIndex + 1;
    },
    prevGlasses() {
      if (this.currentGlassesIndex - 1 === -1) {
        this.currentGlassesIndex = GLASSES.length - 1;
        return;
      }

      this.currentGlassesIndex = this.currentGlassesIndex - 1;
    },
    nextHair() {
      if (this.currentHairIndex + 1 === HAIR.length) {
        this.currentHairIndex = 0;
        return;
      }

      this.currentHairIndex = this.currentHairIndex + 1;
    },
    prevHair() {
      if (this.currentHairIndex - 1 === -1) {
        this.currentHairIndex = HAIR.length - 1;
        return;
      }

      this.currentHairIndex = this.currentHairIndex - 1;
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  overflow-y: hidden;
}

html,
body,
.app {
  width: 100%;
  height: 100%;
  background: url("./assets/prezidentura.jpeg") center center no-repeat;
}

.nauseda-container {
  position: relative;
  min-height: 250px;
  min-width: 250px;
  width: auto;
  height: 840px;
}

.nauseda {
  position: relative;
}

.glasses {
  position: absolute;
  top: 340px;
  left: 315px;
  z-index: 10;

  &--1 {
    top: 340px;
    left: 315px;
  }

  &--2 {
    top: 270px;
    left: 375px;
  }

  &--3 {
    top: 350px;
    left: 385px;
  }

  &--4 {
    top: 300px;
    left: 390px;
  }
}

.hair {
  position: absolute;
  top: 340px;
  left: 315px;
  z-index: 10;
  &--1 {
    top: 110px;
    left: 245px;
  }

  &--2 {
    top: 80px;
    left: 275px;
  }

  &--3 {
    top: 142px;
    left: 179px;
  }

  &--4 {
    top: 300px;
    left: 390px;
  }
}

.app {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.sunglass-control-right {
  z-index: 10;
  cursor: pointer;
  position: absolute;
  width: 60px;
  height: 60px;
  top: 360px;
  right: 770px;
  transform: rotate(180deg);
}
.sunglass-control-left {
  z-index: 10;
  cursor: pointer;
  position: absolute;
  width: 60px;
  height: 60px;
  top: 360px;
  left: 770px;
}

.hair-control-right {
  z-index: 10;
  cursor: pointer;
  position: absolute;
  width: 60px;
  height: 60px;
  top: 240px;
  right: 770px;
  transform: rotate(180deg);
}
.hair-control-left {
  z-index: 10;
  cursor: pointer;
  position: absolute;
  width: 60px;
  height: 60px;
  top: 240px;
  left: 770px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
