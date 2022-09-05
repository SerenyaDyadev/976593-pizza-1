<template>
  <div>
    <label
      v-for="size in sizesList"
      :key="size.id"
      class="diameter__input"
      :class="{
        'diameter__input--small': size.name === '23 см',
        'diameter__input--normal': size.name === '32 см',
        'diameter__input--big': size.name === '45 см',
      }"
      @click="$emit('updateOrder', { name: 'size', value: size.name })"
    >
      <radio-button name="size" :value="order.size" />
      <span>{{ size.name }}</span>
    </label>
  </div>
</template>

<script>
import RadioButton from "@/common/components/RadioButton";

export default {
  name: "BuilderSizeSelector",
  components: {
    RadioButton,
  },
  props: {
    sizesList: {
      type: Array,
      required: true,
      default: () => [],
    },
    order: {
      type: Object,
      require: true,
    },
  },
  methods: {
    doughName(name) {
      return name === "Тонкое" ? "light" : "large";
    },
  },
};
</script>
