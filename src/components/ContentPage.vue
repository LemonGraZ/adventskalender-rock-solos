<template>
  <div class="fill-width fill-height bg">
    <TodayBanner v-if="currentDay != (new Date()).getDate()" />
    <QuestionFrame
      v-if="currentDay >= 1 && currentDay <= 24 && !isInFuture"
      :day="currentDay"
    />
    <InFuture v-if="isInFuture" />
  </div>
</template>

<script>
import { useRouter } from "vue-router";

export default {
  data: () => ({
    currentDay: new Date().getDate(),
  }),
  created() {
    const router = useRouter();
    if (!router.currentRoute.value.params.day) {
      router.push(`/day/${this.currentDay}`);
    } else {
      this.currentDay = parseInt(router.currentRoute.value.params.day);
    }
  },
  computed: {
    isInFuture() {
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      const chosenDate = new Date(2024, 11, this.currentDay);
      console.log(chosenDate);
      console.log(today);
      return chosenDate.getTime() > today.getTime();
    },
  },
};
</script>

<style>
.bg {
  background-color: #063125;
  background: linear-gradient(
    0deg,
    rgba(4, 33, 25, 1) 8%,
    rgba(8, 65, 49, 1) 86%
  );
}
</style>
