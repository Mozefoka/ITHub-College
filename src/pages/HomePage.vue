<script setup lang="ts">
import BaseHero from '@/components/BaseHero.vue'
import CollegeInfo from '@/components/CollegeInfo.vue'
import InviteSection from '@/components/InviteSection.vue'
import BenefitsSection from '@/components/BenefitsSection.vue'
import SuccessStories from '@/components/SuccessStories.vue'
import PracticeSection from '@/components/PracticeSection.vue'
import GallerySection from '@/components/GallerySection.vue'
import StudyDirections from '@/components/StudyDirections.vue'
</script>

<template>
  <BaseHero video="https://kinescope.io/sVCpxzJmjX6355Tr83pE7F" type="iframe" />
  <CollegeInfo />
  <InviteSection />
  <BenefitsSection />
  <SuccessStories :star="icons.star"/>
  <PracticeSection />
  <GallerySection />
  <StudyDirections />
</template>

<style lang="scss" scoped></style>
