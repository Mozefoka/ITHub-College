<script setup lang="ts">
interface ButtonProps {
  text: string
  size?: 'large' | 'medium' | 'small'
  variant?: 'purple' | 'transparent'
}

const props = withDefaults(defineProps<ButtonProps>(), {
  size: 'medium',
  variant: 'purple',
})
</script>

<template>
  <button class="button-cta" :class="[`button-cta--${props.size}`, `button-cta--${props.variant}`]">
    {{ props.text }}
  </button>
</template>

<style scoped lang="scss">
.button-cta {
  width: 100%;
  font-weight: 600;
  border-radius: 10px;
  color: $color-white;

  &--large {
    padding: 22px;
  }

  &--medium {
    padding: 17px 20px;
    font-size: 15px;
  }

  &--small {
    padding: 12px 20px;
  }

  &--purple {
    background-color: $color-purple;
  }

  &--transparent {
    position: relative;
    color: $color-black;
    border: 1px solid $color-black;
    background-color: transparent;
    transition: $transition;
    filter: invert(1);

    &:hover {
      filter: invert(0);
      background-color: $color-white;
    }

    &:after {
      content: '';
      width: 20px;
      height: 20px;
      padding-right: 30px;
      position: absolute;
      top: 50%;
      right: 0;
      transform: translateY(-50%);
      background: url('@/assets/icons/btn-arrow.svg') no-repeat;
    }
  }
}
</style>
