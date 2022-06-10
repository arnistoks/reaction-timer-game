<template>
  <p>Reaction time: {{ score }}ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ResultsComponent",
  props: ["score"],
  data: () => ({
    rank: "",
  }),
  mounted() {
    if (this.score < 250) {
      this.rank = "Ninja Fingers";
    } else if (this.score < 400) {
      this.rank = "Rapid Reflexes";
    } else {
      this.rank = "Snail pace...";
    }
  },
});
</script>

<style scoped lang="scss">
.rank {
  font-size: 1.4em;
  color: #0faf87;
  font-weight: bold;
}
</style>
