<script setup lang="ts">
import ButtonCta from '@/components/ui/ButtonCta.vue'
import BaseSlider from '@/components/BaseSlider.vue'

interface Tag {
  id: number
  name: string
}

interface Video {
  video: string
}

const props = defineProps<Video>()

const tags: Tag[] = [
  {
    id: 1,
    name: 'Информационная безопасность',
  },

  {
    id: 2,
    name: 'Программирование и управление ИТ-продуктом',
  },

  {
    id: 3,
    name: 'Дизайн',
  },

  {
    id: 4,
    name: 'Разработка игр',
  },

  {
    id: 5,
    name: 'Маркетинг и коммерция',
  },
]
</script>

<template>
  <section class="hero">
    <div class="container">
      <div class="hero__inner">
        <div class="hero__content">
          <div class="hero__text">
            <p class="hero__eyebrow">Колледж информационных и креативных технологий</p>
            <h1 class="hero__title">Колледж IThub в Санкт-Петербурге</h1>
          </div>

          <div class="hero__actions">
            <div class="hero__btn">
              <ButtonCta text="ПОДАТЬ ДОКУМЕНТЫ" />
            </div>

            <div class="hero__btn">
              <ButtonCta text="КОНСУЛЬТАЦИЯ ПО ПОСТУПЛЕНИЮ" variant="transparent" />
            </div>
          </div>

          <ul class="hero__tags">
            <li v-for="tag in tags" class="hero__tag" :key="tag.id">
              <a href="#">{{ tag.name }}</a>
            </li>
          </ul>
        </div>

        <div class="hero__gallery">
          <div class="hero__gallery-group">
            <img
              :src="images.students"
              class="hero__gallery-group-item hero__gallery-group-item--first"
              alt="Студенты"
            />
            <img
              :src="images.students2"
              class="hero__gallery-group-item hero__gallery-group-item--second"
              alt="Студенты"
            />
            <div class="hero__gallery-group-item hero__gallery-group-item--third">
              <BaseSlider :images="[images.students, images.students2, images.students3]" />
            </div>
          </div>

          <div class="hero__gallery-badge-image">
            <img :src="images.students2" alt="Студенты" />
          </div>

          <div class="hero__gallery-video">
            <video
              v-if="props.video.endsWith('.mp4')"
              class="hero__gallery-video-item"
              :src="props.video"
              autoplay
              muted
              loop
              playsinline
            />
            <iframe
              v-else
              class="hero__gallery-video-item"
              :src="`${props.video}?background=1`"
              allow="autoplay"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
.hero {
  &__inner {
  }

  &__content {
  }

  &__text {
  }

  &__eyebrow {
  }

  &__title {
  }

  &__actions {
  }

  &__btn {
  }

  &__tags {
  }

  &__tag {
  }

  &__gallery {
  }

  &__gallery-group {
  }

  &__gallery-group-item {
    &--first {
    }

    &--second {
    }

    &--third {
    }
  }

  &__gallery-badge-image {
  }

  &__gallery-video {
  }

  &__gallery-video-item {
  }
}
</style>
