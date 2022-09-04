<template>
  <h1 v-if="big" class="title title--big">{{ title }}</h1>
  <h2 v-else class="title title--small">{{ title }}</h2>
</template>

<script>
export default {
  name: "AppTitle",
  props: {
    title: {
      type: String,
      required: true,
    },
    big: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  box-sizing: border-box;
  width: 100%;
  margin: 0;

  color: $black;

  &--big {
    @include b-s36-h42;
  }

  &--small {
    @include b-s18-h21;
  }
}
</style>
