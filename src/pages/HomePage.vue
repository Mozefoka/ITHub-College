<script setup lang="ts">
import BaseHero from '@/components/BaseHero.vue'
import CollegeInfo from '@/components/CollegeInfo.vue'
import InviteSection from '@/components/InviteSection.vue'
import BenefitsSection from '@/components/BenefitsSection.vue'
import SuccessStories from '@/components/SuccessStories.vue'
</script>

<template>
  <BaseHero video="https://kinescope.io/sVCpxzJmjX6355Tr83pE7F" />
  <CollegeInfo />
  <InviteSection />
  <BenefitsSection />
  <SuccessStories :star="icons.star"/>
</template>

<style lang="scss" scoped></style>
