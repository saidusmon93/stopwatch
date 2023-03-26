<template>
  <div class="container">
    <div class="row">
      <div class="column-sm column-md column-lg position">
        <Stopwatch />
      </div>
      <div
        class="column-sm column-md column-lg position"
        v-for="(stopwatch, index) in stopwatches"
        :key="index"
      >
        <Stopwatch />
      </div>
      <div class="column-sm column-md column-lg position">
        <div class="stopwatch" @click="add">
          <img src="../assets/img/add.png" alt="add" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Stopwatch from "@/components/Stopwatch.vue";

export default {
  name: "Home",
  components: {
    Stopwatch,
  },
  data() {
    return {
      stopwatches: [],
    };
  },

  methods: {
    add() {
      this.stopwatches.push(Stopwatch);
    },
  },
};
</script>
