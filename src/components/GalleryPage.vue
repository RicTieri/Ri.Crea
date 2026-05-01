<script setup lang="ts">
defineProps<{
  gallery: {
    slug: string
    label: string
    title: string
    intro: string
    images: Array<{ src: string; caption: string; tag: string }>
  }
}>()

defineEmits<{
  'back': []
}>()
</script>

<template>
  <div class="gallery-page-view">
    <div class="gallery-hero">
      <button class="back-link" @click="$emit('back')">
        <span>←</span> Torna al portfolio
      </button>
      <span class="eyebrow">Selezione</span>
      <h1>{{ gallery.title }}</h1>
      <p>{{ gallery.intro }}</p>
    </div>
    <div class="gallery-grid">
      <article
        v-for="(image, index) in gallery.images"
        :key="image.src"
        :class="['gallery-card', { 'gallery-card--large': index % 5 === 0 || index % 5 === 3 }]"
      >
        <div class="gallery-card-image" :style="{ backgroundImage: `url(${image.src})` }"></div>
        <div class="gallery-card-copy">
          <span class="eyebrow">{{ image.tag }}</span>
          <p>{{ image.caption }}</p>
        </div>
      </article>
    </div>
  </div>
</template>

<style scoped>
.gallery-page-view {
  min-height: 100vh;
  padding: clamp(60px, 8vw, 100px) 0;
}

.gallery-hero {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 28px;
  margin-bottom: 60px;
}

.back-link {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: none;
  border: none;
  color: var(--accent);
  font-size: 0.88rem;
  font-weight: 600;
  text-transform: uppercase;
  cursor: pointer;
  margin-bottom: 28px;
  transition: all 0.3s ease;
  font-family: inherit;
}

.back-link:hover {
  transform: translateX(-4px);
}

.gallery-hero .eyebrow {
  display: block;
  margin-bottom: 16px;
}

.gallery-hero h1 {
  margin: 0 0 24px;
  font-family: var(--heading);
  font-size: clamp(2.5rem, 4vw, 3.5rem);
  line-height: 1.1;
  color: var(--text-strong);
  font-weight: 400;
}

.gallery-hero p {
  max-width: 700px;
  color: var(--text-muted);
  font-size: 1rem;
  line-height: 1.8;
}

.gallery-grid {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 28px;
  display: grid;
  grid-template-columns: repeat(12, minmax(0, 1fr));
  gap: 20px;
  align-items: stretch;
}

.gallery-card {
  position: relative;
  overflow: hidden;
  border-radius: 28px;
  min-height: 340px;
  display: grid;
  grid-template-rows: 1fr auto;
  background: var(--surface);
  box-shadow: 0 24px 64px rgba(0, 0, 0, 0.24);
}

.gallery-card--large {
  grid-column: span 7;
  min-height: 420px;
}

.gallery-card:not(.gallery-card--large) {
  grid-column: span 5;
}

.gallery-card-image {
  background-size: cover;
  background-position: center;
  filter: saturate(1.05) contrast(1.03);
  min-height: 260px;
}

.gallery-card-copy {
  padding: 24px;
  display: grid;
  gap: 10px;
  background: linear-gradient(180deg, rgba(8, 8, 12, 0.92), rgba(8, 8, 12, 0.72));
}

.gallery-card-copy .eyebrow {
  color: var(--accent);
  font-size: 0.82rem;
}

.gallery-card-copy p {
  margin: 0;
  color: var(--text-muted);
  font-size: 0.96rem;
  line-height: 1.8;
}

@media (max-width: 960px) {
  .gallery-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .gallery-card,
  .gallery-card--large,
  .gallery-card:not(.gallery-card--large) {
    grid-column: span 1;
  }
}

@media (max-width: 640px) {
  .gallery-card {
    min-height: 300px;
  }
}
</style>
