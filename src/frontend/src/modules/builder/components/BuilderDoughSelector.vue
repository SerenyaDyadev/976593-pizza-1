<template>
  <div>
    <label
      v-for="dough in doughList"
      :key="dough.id"
      class="dough__input"
      :class="['dough__input--' + doughName(dough.name)]"
      @click="
        $emit('updateOrder', {
          name: 'dough',
          value: dough.name,
          price: dough.price,
        })
      "
    >
      <radio-button name="dough" :value="order.dough" />
      <b>{{ dough.name }}</b>
      <span>{{ dough.description }}</span>
    </label>
  </div>
</template>

<script>
import RadioButton from "@/common/components/RadioButton";

export default {
  name: "BuilderDoughSelector",
  components: {
    RadioButton,
  },
  props: {
    doughList: {
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
