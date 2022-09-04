<template>
  <input
    type="radio"
    :name="name"
    v-model="valueModel"
    class="visually-hidden"
  />
</template>

<script>
export default {
  name: "RadioButton",
  props: {
    name: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
  },
  computed: {
    valueModel: {
      get() {
        return this.value;
      },
      set() {},
    },
  },
};
</script>

<style lang="scss" scoped>
.visually-hidden {
  position: absolute;

  overflow: hidden;
  clip: rect(0 0 0 0);

  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;

  white-space: nowrap;

  border: 0;

  clip-path: inset(100%);
}
</style>
