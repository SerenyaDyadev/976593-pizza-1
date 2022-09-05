<template>
  <div class="pizza" :class="['pizza--foundation--' + dough + '-' + sauce]">
    <div class="pizza__wrapper">
      <div
        v-for="ingredient in order.ingredients"
        :key="ingredient.id"
        class="pizza__filling"
        :class="[
          `pizza__filling--${ingredientsDictionary[ingredient.id]}`,
          ingredient.count === 2 ? 'pizza__filling--second' : '',
          ingredient.count === 3 ? 'pizza__filling--third' : '',
        ]"
      ></div>
    </div>
  </div>
</template>

<script>
import ingredientsDictionary from "@/common/enums/ingredientsDictionary";

export default {
  name: "BuilderPizzaView",
  data() {
    return {
      ingredientsDictionary,
    };
  },
  props: {
    order: {
      type: Object,
      require: true,
    },
  },
  computed: {
    dough() {
      return this.order.dough === "Толстое" ? "big" : "small";
    },
    sauce() {
      return this.order.sauce === "Томатный" ? "tomato" : "creamy";
    },
  },
};
</script>
