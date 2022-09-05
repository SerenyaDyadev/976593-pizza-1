<template>
  <div id="app">
    <AppLayout
      :pizza="pizza"
      :order="order"
      :orderedArray="orderedArray"
      @updateOrder="updateOrder"
      @toBasket="toBasket"
    />
  </div>
</template>

<script>
import pizza from "@/static/pizza.json";
import AppLayout from "@/layouts/AppLayout";

export default {
  name: "App",
  components: {
    AppLayout,
  },
  data() {
    return {
      pizza,
      orderedArray: [],
      order: {
        name: "",
        dough: "",
        sauce: "",
        size: "",
        ingredients: [],
        priceCounter: 0,
      },
    };
  },
  methods: {
    toBasket() {
      this.orderedArray.push(this.order);
      this.order = {
        name: "",
        dough: "",
        sauce: "",
        size: "",
        ingredients: [],
        priceCounter: 0,
      };
    },
    updateOrder(event) {
      console.log("updateOrder: ", event);
      if (event.count) {
        let ingredients = this.order.ingredients;
        const index = ingredients.findIndex(({ id }) => id === event.id);
        if (~index) {
          let count = ingredients[index].count + event.count;
          count > 0
            ? ingredients.splice(index, 1, {
                id: event.id,
                name: event.name,
                price: event.price,
                count: count,
              })
            : ingredients.splice(index, 1);
        } else {
          ingredients.push({
            id: event.id,
            name: event.name,
            price: event.price,
            count: event.count,
          });
        }
      }

      switch (event.name) {
        case "size":
          this.order.size = event.value;
          break;
        case "name":
          this.order.name = event.namePizza;
          break;
        case "dough":
          this.order.dough = event.value;
          this.order.doughPrice = event.price;
          break;
        case "sauce":
          this.order.sauce = event.value;
          this.order.saucePrice = event.price;
          break;
        default:
          this.order;
      }

      //Price
      let ingredientsPrice = 0;
      if (this.order.ingredients) {
        for (let ingredient of this.order.ingredients) {
          ingredientsPrice += ingredient.price * ingredient.count;
        }
      }

      this.order.priceCounter = [
        this.order.doughPrice,
        this.order.saucePrice,
        ingredientsPrice,
      ]
        .filter((num) => num)
        .reduce((acc, num) => acc + num, 0);
    },
  },
};
</script>

<style lang="scss">
@import "~@/assets/scss/app";
</style>
