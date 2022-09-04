<template>
  <main class="content">
    <form action="#" method="post">
      <div class="content__wrapper">
        <AppTitle title="Конструктор пиццы" big />
        <div class="content__dough">
          <div class="sheet">
            <AppTitle class="sheet__title" title="Выберите тесто" />
            <BuilderDoughSelector
              class="sheet__content dough"
              :dough-list="pizza.dough"
              :order="order"
              @updateOrder="$emit('updateOrder', $event)"
            />
          </div>
        </div>

        <div class="content__diameter">
          <div class="sheet">
            <AppTitle class="sheet__title" title="Выберите размер" />
            <BuilderSizeSelector
              class="sheet__content diameter"
              :sizes-list="pizza.sizes"
              :order="order"
              @updateOrder="$emit('updateOrder', $event)"
            />
          </div>
        </div>
        <div class="content__ingredients">
          <div class="sheet">
            <AppTitle class="sheet__title" title="Выберите ингредиенты" />
            <BuilderIngredientsSelector
              class="sheet__content ingredients"
              :sauces-list="pizza.sauces"
              :ingredients-list="pizza.ingredients"
              :order="order"
              @updateOrder="$emit('updateOrder', $event)"
            />
          </div>
        </div>

        <div class="content__pizza">
          <label class="input">
            <span class="visually-hidden">Название пиццы</span>
            <input
              type="text"
              name="pizza_name"
              :value="order.namePizza"
              @input="
                $emit('updateOrder', {
                  name: 'name',
                  namePizza: $event.target.value,
                })
              "
              placeholder="Введите название пиццы"
            />
          </label>

          <AppDrop @drop="$emit('updateOrder', $event)">
            <div class="content__constructor">
              <BuilderPizzaView :order="order" />
            </div>
          </AppDrop>

          <BuilderPriceCounter
            class="content__result"
            :priceCounter="order.priceCounter"
          />
        </div>
      </div>
    </form>
  </main>
</template>

<script>
import AppTitle from "@/common/components/AppTitle";
import AppDrop from "@/common/components/AppDrop";
import BuilderDoughSelector from "@/modules/builder/components/BuilderDoughSelector";
import BuilderSizeSelector from "@/modules/builder/components/BuilderSizeSelector";
import BuilderIngredientsSelector from "@/modules/builder/components/BuilderIngredientsSelector";
import BuilderPizzaView from "@/modules/builder/components/BuilderPizzaView";
import BuilderPriceCounter from "@/modules/builder/components/BuilderPriceCounter";

export default {
  name: "IndexHome",
  components: {
    AppTitle,
    AppDrop,
    BuilderDoughSelector,
    BuilderSizeSelector,
    BuilderIngredientsSelector,
    BuilderPizzaView,
    BuilderPriceCounter,
  },
  // data() {
  //   return {
  //     priceCounter: 0,
  //   };
  // },
  props: {
    pizza: {
      type: Object,
      require: true,
    },
    order: {
      type: Object,
      require: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  padding-top: 20px;
}

.content__wrapper {
  display: flex;
  align-items: flex-start;
  flex-wrap: wrap;

  width: 920px;
  margin: 0 auto;
  padding-right: 2.12%;
  padding-bottom: 30px;
  padding-left: 2.12%;
}

.content__dough {
  width: 527px;
  margin-top: 15px;
  margin-right: auto;
  margin-bottom: 15px;
}

.content__diameter {
  width: 373px;
  margin-top: 15px;
  margin-bottom: 15px;
}

.content__ingredients {
  width: 527px;
  margin-top: 15px;
  margin-right: auto;
  margin-bottom: 15px;
}

.content__pizza {
  width: 373px;
  margin-top: 15px;
  margin-bottom: 15px;
}

.content__constructor {
  width: 315px;
  margin-top: 25px;
  margin-right: auto;
  margin-left: auto;
}

.content__result {
  display: flex;
  align-items: center;
  justify-content: center;

  margin-top: 25px;

  p {
    @include b-s24-h28;

    margin: 0;
  }

  button {
    margin-left: 12px;
    padding: 16px 45px;
  }
}
</style>
