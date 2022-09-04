<template>
  <div>
    <p>Итого: {{ priceCounter }} ₽</p>
    <button type="button" class="button" :disabled="disabled">Готовьте!</button>
  </div>
</template>

<script>
export default {
  name: "BuilderPriceCounter",
  props: {
    priceCounter: {
      type: Number,
      require: true,
    },
  },
  computed: {
    disabled() {
      return this.priceCounter === 0;
    },
  },
};
</script>

<style lang="scss" scoped></style>
