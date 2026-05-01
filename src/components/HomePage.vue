<script setup lang="ts">
import { onMounted } from 'vue'

defineProps<{
  galleryItems: Array<{ slug: string; title: string; category: string; description: string; image: string }>
  services: Array<{ slug: string; title: string; details: string; image: string }>
  particles: Array<any>
}>()

defineEmits<{
  'open-gallery': [slug: string]
  'open-service': [slug: string]
}>()

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view')
          observer.unobserve(entry.target)
        }
      })
    },
    {
      threshold: 0.16,
      rootMargin: '0px 0px -80px 0px',
    }
  )

  document.querySelectorAll('.reveal, .editorial-card, .service-card').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<template>
  <div class="site-shell">
    <div class="ambient-layer" aria-hidden="true">
      <span
        v-for="particle in particles"
        :key="`${particle.x}-${particle.y}`"
        class="particle"
        :class="`is-${particle.color}`"
        :style="{
          '--x': `${particle.x}%`,
          '--y': `${particle.y}%`,
          '--size': `${particle.size}px`,
          '--drift': `${particle.drift}px`,
          '--delay': particle.delay,
        }"
      ></span>
      <span class="light-trail trail-one"></span>
      <span class="light-trail trail-two"></span>
    </div>

    <header class="hero-section">
      <div class="hero-content">
        <div class="hero-text">
          <div class="hero-logo-wrap" aria-label="Ri.Crea">
            <img class="hero-logo" src="/logo.png" alt="" />
          </div>
          <span class="eyebrow">Portfolio fotografico per brand e attività</span>
          <h1>Fotografia per<br>aziende e locali.</h1>
          <p>Servizi fotografici editoriali e narrativi per eventi aziendali, ritratti professionali, brand, attività e locali che desiderano raccontare con autenticità.</p>
          <div class="hero-meta" aria-label="Dettagli portfolio">
            <span>Editoriale</span>
            <span>Ritratti</span>
            <span>Eventi aziendali</span>
          </div>
          <div class="hero-actions hero-actions-desktop">
            <a class="button primary" href="#contact">Prenota</a>
            <a class="button ghost" href="#portfolio">Portfolio</a>
          </div>
        </div>
        <div class="hero-images">
          <div class="hero-kicker">
            <span>Ri.Crea</span>
            <strong>Visual Stories</strong>
          </div>
          <div class="image-layer layer-1"></div>
          <div class="image-layer layer-2"></div>
          <div class="image-layer layer-3"></div>
          <div class="hero-caption">
            <span>Frame 01</span>
            <span>Natural light / cinematic color</span>
          </div>
        </div>
        <div class="hero-actions hero-actions-mobile">
          <a class="button ghost" href="#portfolio">Portfolio</a>
          <a class="button primary" href="#contact">Prenota</a>
        </div>
      </div>
    </header>

    <main>
      <section class="about-section page-section" id="about">
        <div class="section-rail" aria-hidden="true">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="section-intro reveal reveal-up">
          <span class="eyebrow">Sul fotografo</span>
          <h2>Fotografia professionale guidata da atmosfera, composizione e connessioni autentiche.</h2>
          <p>Con un occhio raffinato per colore e narrazione, Ri.Crea realizza immagini per aziende, locali, professionisti e brand che vogliono comunicare con personalità.</p>
        </div>
      </section>

      <section class="editorial-section page-section section-band" id="portfolio">
        <div class="section-rail is-right" aria-hidden="true">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="section-top reveal reveal-left">
          <span class="eyebrow">Selezioni dal portfolio</span>
          <h2>Lavori scelti tra ritrattistica, eventi aziendali, locali e campagne creative.</h2>
        </div>
        <div class="editorial-grid">
          <article v-for="(item, index) in galleryItems" :key="item.title" class="editorial-card">
            <div class="editorial-image" :style="{ backgroundImage: `url(${item.image})` }"></div>
            <span class="work-index">{{ String(index + 1).padStart(2, '0') }}</span>
            <div class="editorial-copy">
              <span class="eyebrow">{{ item.category }}</span>
              <h3>{{ item.title }}</h3>
              <p>{{ item.description }}</p>
              <a
                class="service-link"
                href="javascript:void(0)"
                @click.prevent="$emit('open-gallery', item.slug)"
              >
                Vai alla galleria
              </a>
            </div>
          </article>
        </div>
      </section>

      <section class="services-section page-section" id="services">
        <div class="section-rail" aria-hidden="true">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="section-top reveal reveal-right">
          <span class="eyebrow">Servizi</span>
          <h2 class="services-title">Pacchetti pensati<br><em>e flessibili</em> per ogni progetto.</h2>
        </div>
        <div class="service-grid">
          <article v-for="service in services" :key="service.title" class="service-card">
            <h3>{{ service.title }}</h3>
            <p>{{ service.details }}</p>
            <a
              class="service-link"
              href="javascript:void(0)"
              @click.prevent="$emit('open-service', service.slug)"
            >
              Scopri il servizio
            </a>
          </article>
        </div>
      </section>

      <section class="contact-section page-section section-band" id="contact">
        <div class="contact-card reveal reveal-up">
          <div class="contact-mark" aria-hidden="true"></div>
          <span class="eyebrow">Creiamo insieme</span>
          <h2>Pronto a prenotare il tuo prossimo servizio fotografico?</h2>
          <p>Contattami per disponibilità, tariffe personalizzate o una consulenza creativa per eventi aziendali, locali, ritratti professionali e contenuti visual per brand.</p>
          <a class="button primary" href="mailto:hello@example.com">Email hello@example.com</a>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <img class="footer-logo" src="/logo.png" alt="Ri.Crea" />
      <p>Creata per persone, luoghi e ritratti.</p>
    </footer>
  </div>
</template>
