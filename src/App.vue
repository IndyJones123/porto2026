<script setup lang="ts">
import NavBar from './components/NavBar.vue';
import HeroSection from './components/HeroSection.vue';
import StatsSection from './components/StatsSection.vue';
import ExperienceSection from './components/ExperienceSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import SkillsSection from './components/SkillsSection.vue';
import ContactSection from './components/ContactSection.vue';
import FooterComponent from './components/FooterComponent.vue';
</script>

<template>
  <div class="min-h-screen bg-bg-primary text-text-primary font-sans antialiased overflow-x-hidden">
    <NavBar />
    <HeroSection />
    <StatsSection />
    <ExperienceSection />
    <ProjectsSection />
    <SkillsSection />
    <ContactSection />
    <FooterComponent />
  </div>
</template>

<style>
/* Global styles if needed, but Tailwind handles most */
html {
  scroll-behavior: smooth;
}
</style>
