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
      default: () => {},
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

<style lang="scss" scoped>
@import "../../../assets/scss/mixins/mixins";
.pizza {
  position: relative;

  display: block;

  box-sizing: border-box;
  width: 100%;

  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;

  &--foundation--big-creamy {
    background-image: url("../../../assets/img/foundation/big-creamy.svg");
  }

  &--foundation--big-tomato {
    background-image: url("../../../assets/img/foundation/big-tomato.svg");
  }

  &--foundation--small-creamy {
    background-image: url("../../../assets/img/foundation/small-creamy.svg");
  }

  &--foundation--small-tomato {
    background-image: url("../../../assets/img/foundation/small-tomato.svg");
  }
}

.pizza__wrapper {
  width: 100%;
  padding-bottom: 100%;
}

.pizza__filling {
  $bl: &;
  position: absolute;
  top: 0;
  left: 0;

  display: block;

  width: 100%;
  height: 100%;

  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;

  &::before,
  &::after {
    display: none;

    position: absolute;
    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    content: "";

    background-image: inherit;
  }

  &--second {
    &::before {
      display: block;

      transform: rotate(45deg);
    }
  }

  &--third {
    &::before {
      display: block;

      transform: rotate(45deg);
    }

    &::after {
      display: block;

      transform: rotate(-45deg);
    }
  }

  &--ananas,
  &--ananas.pizza__filling--second::before,
  &--ananas.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/ananas.svg");
  }

  &--bacon,
  &--bacon.pizza__filling--second::before,
  &--bacon.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/bacon.svg");
  }

  &--blue_cheese,
  &--blue.pizza__filling--second::before,
  &--blue.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/blue_cheese.svg");
  }

  &--cheddarcheddar,
  &--cheddar.pizza__filling--second::before,
  &--cheddar.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/cheddar.svg");
  }

  &--chile,
  &--chile.pizza__filling--second::before,
  &--chile.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/chile.svg");
  }

  &--ham,
  &--ham.pizza__filling--second::before,
  &--ham.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/ham.svg");
  }

  &--jalapeno,
  &--jalapeno.pizza__filling--second::before,
  &--jalapeno.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/jalapeno.svg");
  }

  &--mozzarella,
  &--mozzarella.pizza__filling--second::before,
  &--mozzarella.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/mozzarella.svg");
  }

  &--mushrooms,
  &--mushrooms.pizza__filling--second::before,
  &--mushrooms.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/mushrooms.svg");
  }

  &--olives,
  &--olives.pizza__filling--second::before,
  &--olives.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/olives.svg");
  }

  &--onion,
  &--onion.pizza__filling--second::before,
  &--onion.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/onion.svg");
  }

  &--parmesan,
  &--parmesan.pizza__filling--second::before,
  &--parmesan.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/parmesan.svg");
  }

  &--salami,
  &---salami.pizza__filling--second::before,
  &---salami.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/salami.svg");
  }

  &--salmon,
  &--salmon.pizza__filling--second::before,
  &--salmon.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/salmon.svg");
  }

  &--tomatoes,
  &--tomatoes.pizza__filling--second::before,
  &--tomatoes.pizza__filling--third::after {
    background-image: url("../../../assets/img/filling-big/tomatoes.svg");
  }
}
</style>
