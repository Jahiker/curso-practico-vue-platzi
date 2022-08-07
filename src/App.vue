<script>
import SplashScreen from "@/components/SplashScreen.vue";
import { defineAsyncComponent } from "vue";

export default {
  components: {
    SplashScreen,
    Home: defineAsyncComponent(() => {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/Home.vue"));
        }, 2000);
      })
    })
  }
}
</script>

<template>
  <Suspense>
    <Home />
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>

<style scoped>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
}
</style>
