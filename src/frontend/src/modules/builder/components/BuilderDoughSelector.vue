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
      default: () => {},
    },
  },
  methods: {
    doughName(name) {
      return name === "Тонкое" ? "light" : "large";
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../../assets/scss/mixins/mixins";
.dough__input {
  position: relative;

  margin-right: 8%;
  margin-bottom: 20px;
  padding-left: 50px;

  cursor: pointer;

  b {
    @include r-s16-h19;

    &::before {
      @include p_center-v;

      width: 36px;
      height: 36px;

      content: "";
      transition: 0.3s;

      border-radius: 50%;
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
    }
  }

  span {
    @include l-s11-h13;

    display: block;
  }

  &--light {
    b {
      &::before {
        background-image: url("../../../assets/img/dough-light.svg");
      }
    }
  }

  &--large {
    b {
      &::before {
        background-image: url("../../../assets/img/dough-large.svg");
      }
    }
  }

  &:hover {
    b::before {
      box-shadow: $shadow-regular;
    }
  }

  input {
    &:checked + b::before {
      box-shadow: $shadow-large;
    }
  }
}
</style>
