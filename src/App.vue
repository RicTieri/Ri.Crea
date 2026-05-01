<script setup lang="ts">
import { onMounted } from 'vue'

const galleryItems = [
  {
    title: 'Ritratti all\'Ora d\'Oro',
    category: 'Ritratto',
    description: 'Ritratti caldi e cinematografici per editoria e personal branding.',
    image: 'https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=1200&q=80',
  },
  {
    title: 'Lifestyle Urbano',
    category: 'Lifestyle',
    description: 'Fotografia di strada con un taglio contemporaneo e naturale.',
    image: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=1200&q=80',
  },
  {
    title: 'Racconti di Matrimonio',
    category: 'Evento',
    description: 'Momenti senza tempo catturati con eleganza, luce morbida e dettagli autentici.',
    image: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=1200&q=80',
  },
  {
    title: 'Dettagli Fine Art',
    category: 'Fine Art',
    description: 'Composizioni raffinate e immagini artigianali per progetti editoriali.',
    image: 'https://images.unsplash.com/photo-1483985988355-763728e1935b?auto=format&fit=crop&w=1200&q=80',
  },
]

const services = [
  {
    title: 'Sessioni di Ritratto',
    details: 'Ritratti in studio e all\'aperto per persone, coppie e creativi.',
  },
  {
    title: 'Fotografia per Eventi',
    details: 'Copertura elegante per attività e locali, con servizi per eventi privati e lanci commerciali.',
  },
  {
    title: 'Lavoro Commerciale',
    details: 'Storytelling del brand, immagini editoriali e campagne creative.',
  },
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view')
        }
      })
    },
    {
      threshold: 0.1,
      rootMargin: '0px 0px -50px 0px',
    }
  )

  document.querySelectorAll('.editorial-card, .service-card, .section-intro, .about-section').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<template>
  <div class="site-shell">
    <header class="hero-section">
      <div class="hero-content">
        <div class="hero-text">
          <span class="eyebrow">Portfolio fotografico</span>
          <h1>Storie visive<br>in luce.</h1>
          <p>Fotografia editoriale e narrativa per brand, attività e locali che desiderano raccontare con autenticità.</p>
          <div class="hero-actions">
            <a class="button primary" href="#contact">Prenota</a>
            <a class="button ghost" href="#portfolio">Portfolio</a>
          </div>
        </div>
        <div class="hero-images">
          <div class="image-layer layer-1"></div>
          <div class="image-layer layer-2"></div>
          <div class="image-layer layer-3"></div>
        </div>
      </div>
    </header>

    <main>
      <section class="about-section" id="about">
        <div class="section-intro">
          <span class="eyebrow">Sul fotografo</span>
          <h2>Guidato dall'atmosfera, dalla composizione e dalle connessioni autentiche.</h2>
          <p>Con un occhio raffinato per il colore e la narrazione, questo portfolio presenta progetti pensati per rendere ogni immagine personale e senza tempo.</p>
        </div>
      </section>

      <section class="editorial-section" id="portfolio">
        <div class="section-top">
          <span class="eyebrow">Selezioni dal portfolio</span>
          <h2>Lavori scelti tra ritrattistica, eventi e campagne creative.</h2>
        </div>
        <div class="editorial-grid">
          <article v-for="item in galleryItems" :key="item.title" class="editorial-card">
            <div class="editorial-image" :style="{ backgroundImage: `url(${item.image})` }"></div>
            <div class="editorial-copy">
              <span class="eyebrow">{{ item.category }}</span>
              <h3>{{ item.title }}</h3>
              <p>{{ item.description }}</p>
            </div>
          </article>
        </div>
      </section>

      <section class="services-section">
        <div class="section-top">
          <span class="eyebrow">Servizi</span>
          <h2>Pacchetti pensati e flessibili per ogni progetto.</h2>
        </div>
        <div class="service-grid">
          <article v-for="service in services" :key="service.title" class="service-card">
            <h3>{{ service.title }}</h3>
            <p>{{ service.details }}</p>
          </article>
        </div>
      </section>

      <section class="contact-section" id="contact">
        <div class="contact-card">
          <span class="eyebrow">Creiamo insieme</span>
          <h2>Pronto a prenotare la tua prossima sessione?</h2>
          <p>Contattami per disponibilità, tariffe personalizzate o una consulenza creativa. Fotografia che rispecchia la tua visione e personalità.</p>
          <a class="button primary" href="mailto:hello@example.com">Email hello@example.com</a>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <p>Ri.Crea Photography — Creata per persone, luoghi e ritratti.</p>
    </footer>
  </div>
</template>
