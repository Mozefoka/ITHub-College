<script setup lang="ts">
import { computed, nextTick, onBeforeUnmount, onMounted, ref } from 'vue'

interface Props {
  images: string[]
  autoplay?: boolean
  interval?: number
}

const props = withDefaults(defineProps<Props>(), {
  autoplay: true,
  interval: 3000,
})

const currentIndex = ref(1)
const isJumping = ref(false)
const trackRef = ref<HTMLElement | null>(null)

let timer: ReturnType<typeof setInterval> | null = null

const extendedImages = computed(() => {
  if (props.images.length === 0) {
    return []
  }

  return [props.images[props.images.length - 1], ...props.images, props.images[0]]
})

const trackStyle = computed(() => ({
  transform: `translateX(-${currentIndex.value * 100}%)`,
}))

function next(): void {
  if (props.images.length <= 1) return

  currentIndex.value++
}

async function onTransitionEnd(event: TransitionEvent): Promise<void> {
  if (event.propertyName !== 'transform') return

  const total = props.images.length

  if (currentIndex.value !== total + 1) {
    return
  }

  isJumping.value = true
  currentIndex.value = 1

  await nextTick()

  trackRef.value?.offsetHeight

  requestAnimationFrame(() => {
    isJumping.value = false
  })
}

function play(): void {
  if (!props.autoplay || props.images.length <= 1) {
    return
  }

  stop()

  timer = setInterval(() => {
    next()
  }, props.interval)
}

function stop(): void {
  if (timer !== null) {
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
  <div v-if="props.images.length" class="slider" @mouseenter="pause" @mouseleave="resume">
    <div
      ref="trackRef"
      class="slider__track"
      :class="{ 'slider__track_no-transition': isJumping }"
      :style="trackStyle"
      @transitionend="onTransitionEnd"
    >
      <div v-for="(image, index) in extendedImages" :key="index" class="slider__slide">
        <img class="slider__img" :src="image" :alt="`slide-${index}`" />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.slider {
  width: 100%;
  overflow: hidden;

  &__track {
    display: flex;
    width: 100%;
    transition: transform 0.4s ease;
  }

  &__track_no-transition {
    transition: none;
  }

  &__slide {
    flex: 0 0 100%;
    min-width: 0;
  }

  &__img {
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
