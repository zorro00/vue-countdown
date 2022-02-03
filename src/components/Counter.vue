<template>
  <div>
    <h3>Hello from Counter</h3>
    <section
      class="text-3xl flex justify-center content-center flex-col mx-auto text-center"
    >
      <h5 v-if="!expired">Buy Now</h5>
      <h5 v-else>Time is Done</h5>
    </section>
    <section class="text-6xl flex justify-center content-center">
      <div class="days mr-2 relative">
        {{ displayDays }}
        <div class="label text-sm absolute bottom-o">Days</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="hours mr-2 relative">
        {{ displayHours }}
        <div class="label text-sm absolute bottom-o">Hours</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="Minutes mr-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute bottom-o">Minutes</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="seconds mr-2 relative">
        {{ displaySeconds }}
        <div class="label text-sm absolute bottom-o">Seconds</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  props: ["year", "Month", "date", "hour", "minute", "second", "milliesecond"],
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
    };
  },
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
  },
  mounted() {
    this.showRemaining();
  },
  methods: {
    formatNum(num) {
      return num < 10 ? "0" + num : num;
    },
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        const end = new Date(2022, 1, 1, 13, 10, 10, 10);
        const distance = end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true;
          return;
        }
        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.displayDays = this.formatNum(days);
        this.displayHours = this.formatNum(hours);
        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
      }, 1000);
    },
  },
};
</script>

<style lang="scss" scoped></style>
