<template>
  <div>
    <label
      v-for="size in sizesList"
      :key="size.id"
      class="diameter__input"
      :class="{
        'diameter__input--small': size.name === '23 см',
        'diameter__input--normal': size.name === '32 см',
        'diameter__input--big': size.name === '45 см',
      }"
      @click="$emit('updateOrder', { name: 'size', value: size.name })"
    >
      <radio-button name="size" :value="order.size" />
      <span>{{ size.name }}</span>
    </label>
  </div>
</template>

<script>
import RadioButton from "@/common/components/RadioButton";

export default {
  name: "BuilderSizeSelector",
  components: {
    RadioButton,
  },
  props: {
    sizesList: {
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
.diameter__input {
  margin-right: 8.7%;
  margin-bottom: 20px;
  padding-top: 7px;
  padding-bottom: 6px;

  cursor: pointer;

  span {
    @include r-s16-h19;

    position: relative;

    padding-left: 46px;

    &::before {
      @include p_center_v;

      width: 36px;
      height: 36px;

      content: "";
      transition: 0.3s;

      border-radius: 50%;
      background-color: $green-100;
      background-image: url("~@/assets/img/diameter.svg");
      background-repeat: no-repeat;
      background-position: center;
    }
  }

  &:nth-child(3n) {
    margin-right: 0;
  }

  &--small {
    span::before {
      background-size: 18px;
    }
  }

  &--normal {
    span::before {
      background-size: 29px;
    }
  }

  &--big {
    span::before {
      background-size: 100%;
    }
  }

  &:hover {
    span::before {
      box-shadow: $shadow-regular;
    }
  }

  input {
    &:checked + span::before {
      box-shadow: $shadow-large;
    }
  }
}
</style>
