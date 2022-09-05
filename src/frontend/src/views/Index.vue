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
            @toBasket="$emit('toBasket')"
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
