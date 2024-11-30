<script lang="ts">
import Top from './components/Top.vue';

export default {
  name: 'App',
  components: { Top },
  data() {
    return {
      topMsg: 'Searching for Abbys...',
      numAbbys: '',
      abbyCount: 5555,
      doneSearching: false,
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
        } else {
          this.doneSearching = true;
        }
      };

      let numDots = 3;
      const updateProgress = () => {
        this.topMsg = 'Searching for Abbys' + '.'.repeat(numDots);
        switch (numDots) {
          case 3:
            numDots = 0;
            break;
          case 2:
            numDots = 3;
            break;
          case 1:
            numDots = 2;
            break;
          case 0:
            numDots = 1;
            break;
        }
        if (this.abbyCount < 100_000_000_000) {
          setTimeout(updateProgress, 400);
        } else {
          this.topMsg = 'Abby search complete!';
        }
      };

      updateProgress();
      updateNum();
    },
  },
};
</script>

<template>
  <main class="max-w-screen-lg m-auto">
    <Top></Top>
    <div class="my-8 max-w-screen-lg border border-black p-8">
      <div class="m-auto w-4/5">
        <div class="text-4xl my-4">{{ topMsg }}</div>
        <div class="text-4xl text-center my-4">{{ numAbbys }}</div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
