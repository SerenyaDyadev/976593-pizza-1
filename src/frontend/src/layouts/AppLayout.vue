<template>
  <body>
    <AppLayoutHeader :priceCounter="order.priceCounter" />
    <Index
      :pizza="pizza"
      :order="order"
      @updateOrder="$emit('updateOrder', $event)"
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
  // data() {
  //   return {
  //     ingredientsAdded: [],
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
  computed: {},
  methods: {},
};
</script>
