<template>
  <div>
    <Header />
    <div>
      <router-view />
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header";

export default {
  components: {
    Header,
  },
};
</script>

