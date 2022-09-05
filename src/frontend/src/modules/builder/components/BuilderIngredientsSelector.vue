<template>
  <div>
    <div class="ingredients__sauce">
      <p>Основной соус:</p>

      <label
        v-for="sauce in saucesList"
        :key="sauce.id"
        class="radio ingredients__input"
        @click="
          $emit('updateOrder', {
            name: 'sauce',
            value: sauce.name,
            price: sauce.price,
          })
        "
      >
        <radio-button name="sauce" :value="sauce.name" />
        <span>{{ sauce.name }}</span>
      </label>
    </div>

    <div class="ingredients__filling">
      <p>Начинка:</p>

      <ul class="ingredients__list">
        <li
          v-for="ingredient in ingredientsList"
          :key="ingredient.id"
          class="ingredients__item"
        >
          <AppDrag :transferData="addIngredient(ingredient, 1)">
            <span
              :class="`filling--${ingredientsDictionary[ingredient.id]}`"
              class="filling"
            >
              {{ ingredient.name }}
            </span>
          </AppDrag>
          <div class="counter counter--orange ingredients__counter">
            <button
              type="button"
              class="counter__button counter__button--minus"
              @click="$emit('updateOrder', addIngredient(ingredient, -1))"
              :disabled="disabledMinus(ingredient.id)"
            >
              <span class="visually-hidden">Меньше</span>
            </button>
            <input
              type="text"
              name="counter"
              class="counter__input"
              :value="ingredientCounter(ingredient.id)"
            />
            <button
              type="button"
              class="counter__button counter__button--plus"
              @click="$emit('updateOrder', addIngredient(ingredient, 1))"
              :disabled="disabledPlus(ingredient.id)"
            >
              <span class="visually-hidden">Больше</span>
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import RadioButton from "@/common/components/RadioButton";
import ingredientsDictionary from "@/common/enums/ingredientsDictionary";
import AppDrag from "@/common/components/AppDrag";

export default {
  name: "BuilderIngredientsSelector",
  components: {
    RadioButton,
    AppDrag,
  },
  data() {
    return {
      ingredientsDictionary,
    };
  },
  props: {
    saucesList: {
      type: Array,
      required: true,
      default: () => [],
    },
    ingredientsList: {
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
    addIngredient(ingredient, count) {
      return {
        id: ingredient.id,
        name: ingredient.name,
        price: ingredient.price,
        count: count,
      };
    },
    findIndex(ingridientId) {
      return this.order.ingredients.findIndex(({ id }) => id === ingridientId);
    },
    ingredientCounter(ingridientId) {
      const index = this.findIndex(ingridientId);
      return ~index ? this.order.ingredients[index].count : 0;
    },
    disabledMinus(ingridientId) {
      const index = this.findIndex(ingridientId);
      return ~index ? !this.order.ingredients[index].count > 0 : true;
    },
    disabledPlus(ingridientId) {
      const index = this.findIndex(ingridientId);
      return ~index ? this.order.ingredients[index].count > 2 : false;
    },
  },
};
</script>
