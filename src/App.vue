<script lang="ts">
import Headline from './components/Headline.vue';

export default {
  name: 'App',
  components: { Headline },
  data() {
    return {
      topMsg: 'Searching for Abbys...',
      numAbbys: '',
      abbyCount: 5555,
    };
  },
  mounted() {
    this.startAnimation();
  },
  methods: {
    startAnimation() {
      const MAX_DELAY = 500;
      const MAX_NUM_DELAYS = 4;

      let numDelays = 0;
      let delay = 0;
      let delayDirection = 1;
      const updateNum = () => {
        this.abbyCount += Math.floor(Math.random() * this.abbyCount * 0.08);
        this.numAbbys = `Found ${this.abbyCount} Abbys in the Universe`;
        if (this.abbyCount < 100_000_000_000) {
          const timeout = Math.floor(Math.random() * 30);
          if (numDelays < MAX_NUM_DELAYS && Math.random() > 0.99) {
            numDelays += 1;
            if (delayDirection === 1) {
              delay = 50;
            } else {
              delay = MAX_DELAY;
            }
          }
          if (delay > MAX_DELAY) {
            delay = MAX_DELAY;
            delayDirection = -1;
          } else if (delay < 15) {
            delay = 0;
            delayDirection = 1;
          }
          const scale = Math.pow(1.7, delayDirection);
          delay = delay + delay * scale * delayDirection;
          setTimeout(updateNum, timeout + delay);
        }
      };

      updateNum();
    },
  },
};
</script>

<template>
  <main>
    <Headline :msg="topMsg"></Headline>
    <Headline v-if="numAbbys" :msg="numAbbys"></Headline>
  </main>
</template>

<style scoped></style>
