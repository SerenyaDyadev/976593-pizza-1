<template>
  <body>
    <AppLayoutHeader :ordered-array="orderedArray" />
    <Index
      :pizza="pizza"
      :order="order"
      @updateOrder="$emit('updateOrder', $event)"
      @toBasket="$emit('toBasket')"
    />
  </body>
</template>

<script>
import AppLayoutHeader from "./AppLayoutHeader";
import Index from "@/views/Index.vue";
export default {
  name: "AppLayout",
  components: {
    Index,
    AppLayoutHeader,
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
    orderedArray: {
      type: Array,
      require: false,
    },
  },
};
</script>
