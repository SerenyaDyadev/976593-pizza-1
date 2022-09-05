<template>
  <div>
    <p>Итого: {{ priceCounter }} ₽</p>
    <button
      type="button"
      class="button"
      :disabled="disabled"
      @click="$emit('toBasket')"
    >
      Готовьте!
    </button>
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
  // methods: {
  //   sendOrder() {
  //     console.log('sendOrder: ');
  //     this.$emit('sendToPay', this.order);
  //   }
  // }
};
</script>
