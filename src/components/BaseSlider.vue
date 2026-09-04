<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

interface Props {
  images: string[]
  autoplay?: boolean
  interval?: number
}

const props = withDefaults(defineProps<Props>(), {
  autoplay: true,
  interval: 3000,
})

// внутреннее состояние компонента — снаружи никак не управляется (uncontrolled)
const currentIndex = ref(1) // 1, т.к. в начале стоит клон последнего слайда
const isJumping = ref(false)
let timer: ReturnType<typeof setInterval> | null = null

// [clone last, ...images, clone first] — приём для бесшовного loop
const extendedImages = computed(() => {
  if (props.images.length === 0) return []
  const first = props.images[0]
  const last = props.images[props.images.length - 1]
  return [last, ...props.images, first]
})

const trackStyle = computed(() => ({
  transform: `translateX(-${currentIndex.value * 100}%)`,
}))

function next(): void {
  currentIndex.value++
}

function onTransitionEnd(): void {
  const total = props.images.length

  if (currentIndex.value === total + 1) {
    isJumping.value = true
    currentIndex.value = 1
  } else if (currentIndex.value === 0) {
    isJumping.value = true
    currentIndex.value = total
  }

  if (isJumping.value) {
    requestAnimationFrame(() => {
      isJumping.value = false
    })
  }
}

function play(): void {
  if (!props.autoplay) return
  stop()
  timer = setInterval(next, props.interval)
}

function stop(): void {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

function pause(): void {
  stop()
}

function resume(): void {
  play()
}

onMounted(play)
onBeforeUnmount(stop)
</script>

<template>
  <div class="slider" @mouseenter="pause" @mouseleave="resume">
    <div
      class="slider__track"
      :class="{ 'slider__track_no-transition': isJumping }"
      :style="trackStyle"
      @transitionend="onTransitionEnd"
    >
      <div v-for="(image, i) in extendedImages" :key="i" class="slider__slide">
        <img class="slider__img" :src="image" :alt="`slide-${i}`" />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.slider {
  position: relative;
  overflow: hidden;
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 12px;

  &__track {
    display: flex;
    height: 100%;
    transition: transform 0.4s ease;

    &_no-transition {
      transition: none;
    }
  }

  &__slide {
    flex: 0 0 100%;
    height: 100%;
  }

  &__img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
}
</style>
