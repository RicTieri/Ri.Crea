<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import HomePage from './components/HomePage.vue'
import GalleryPage from './components/GalleryPage.vue'
import Navigation from './components/Navigation.vue'

const galleryItems = [
  {
    slug: 'ritratti',
    title: 'Ritratti all\'Ora d\'Oro',
    category: 'Ritratto',
    description: 'Ritratti caldi e cinematografici per editoria e personal branding.',
    image: 'https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=1200&q=80',
  },
  {
    slug: 'lifestyle',
    title: 'Lifestyle Urbano',
    category: 'Lifestyle',
    description: 'Fotografia di strada con un taglio contemporaneo e naturale.',
    image: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=1200&q=80',
  },
  {
    slug: 'corporate',
    title: 'Eventi Aziendali',
    category: 'Corporate',
    description: 'Reportage visivi per inaugurazioni, lanci, team event e serate di brand.',
    image: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=1200&q=80',
  },
  {
    slug: 'fine-art',
    title: 'Dettagli Fine Art',
    category: 'Fine Art',
    description: 'Composizioni raffinate e immagini artigianali per progetti editoriali.',
    image: 'https://images.unsplash.com/photo-1483985988355-763728e1935b?auto=format&fit=crop&w=1200&q=80',
  },
]

const portfolioCollections = [
  {
    slug: 'ritratti',
    label: 'Ritratti',
    title: 'Ritratti editoriali',
    intro: 'Una galleria contemporanea di ritratti con luce naturale, composizione cinematografica e dettagli autentici.',
    images: [
      { src: 'https://images.unsplash.com/photo-1500534314209-a25ddb2bd429?auto=format&fit=crop&w=1400&q=80', caption: 'Ritratto ambientato con luce dorata', tag: 'Ritratto' },
      { src: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=1400&q=80', caption: 'Primo piano elegante e naturale', tag: 'Ritratto' },
      { src: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=1400&q=80', caption: 'Scatto editoriale per personal branding', tag: 'Ritratto' },
      { src: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=1400&q=80', caption: 'Ritratto con atmosfera morbida', tag: 'Ritratto' },
      { src: 'https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=1400&q=80', caption: 'Immagine editoriale in interni', tag: 'Ritratto' },
    ],
  },
  {
    slug: 'lifestyle',
    label: 'Lifestyle',
    title: 'Lifestyle urbano',
    intro: 'Una galleria di scatti lifestyle che raccontano movimento, dettagli di strada e personalità moderna.',
    images: [
      { src: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=1400&q=80', caption: 'Cattura spontanea in strada', tag: 'Lifestyle' },
      { src: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=1400&q=80', caption: 'Atteggiamento contemporaneo e grafico', tag: 'Lifestyle' },
      { src: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=1400&q=80', caption: 'Ritratto lifestyle in ambiente urbano', tag: 'Lifestyle' },
      { src: 'https://images.unsplash.com/photo-1483985988355-763728e1935b?auto=format&fit=crop&w=1400&q=80', caption: 'Dettagli di styling e luce naturale', tag: 'Lifestyle' },
      { src: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=1400&q=80', caption: 'Scena dinamica con colore e movimento', tag: 'Lifestyle' },
    ],
  },
  {
    slug: 'corporate',
    label: 'Corporate',
    title: 'Eventi aziendali',
    intro: 'Storytelling visivo per eventi corporate con attenzione all’atmosfera, ai dettagli e alle relazioni tra le persone.',
    images: [
      { src: 'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1400&q=80', caption: 'Copertura elegante dell’evento', tag: 'Corporate' },
      { src: 'https://images.unsplash.com/photo-1515378791036-0648a3ef77b2?auto=format&fit=crop&w=1400&q=80', caption: 'Dettagli del locale e ospiti', tag: 'Corporate' },
      { src: 'https://images.unsplash.com/photo-1497366811353-6870744d04b2?auto=format&fit=crop&w=1400&q=80', caption: 'Immagine istituzionale e narrativa', tag: 'Corporate' },
      { src: 'https://images.unsplash.com/photo-1518609878373-06d740f60d8b?auto=format&fit=crop&w=1400&q=80', caption: 'Scena di networking con luce calda', tag: 'Corporate' },
      { src: 'https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=1400&q=80', caption: 'Atmosfera professionale senza pose forzate', tag: 'Corporate' },
    ],
  },
  {
    slug: 'fine-art',
    label: 'Fine Art',
    title: 'Dettagli fine art',
    intro: 'Una selezione di immagini fine art pensate per progetti editoriali, brand e contenuti di forte impatto visivo.',
    images: [
      { src: 'https://images.unsplash.com/photo-1491553895911-0055eca6402d?auto=format&fit=crop&w=1400&q=80', caption: 'Composizione raffinata e minimal', tag: 'Fine Art' },
      { src: 'https://images.unsplash.com/photo-1500534314209-a25ddb2bd429?auto=format&fit=crop&w=1400&q=80', caption: 'Dettagli artigianali e atmosfera', tag: 'Fine Art' },
      { src: 'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1400&q=80', caption: 'Tono ricercato e luci morbide', tag: 'Fine Art' },
      { src: 'https://images.unsplash.com/photo-1515378791036-0648a3ef77b2?auto=format&fit=crop&w=1400&q=80', caption: 'Porzioni di immagine narrative', tag: 'Fine Art' },
      { src: 'https://images.unsplash.com/photo-1497366811353-6870744d04b2?auto=format&fit=crop&w=1400&q=80', caption: 'Immagine editoriale dal ritmo visivo forte', tag: 'Fine Art' },
    ],
  },
]

const selectedGallerySlug = ref('')
const selectedGallery = computed(() => portfolioCollections.find((collection) => collection.slug === selectedGallerySlug.value))

const currentPage = ref('home')

const syncRouteFromHash = () => {
  const hash = window.location.hash.slice(1)
  if (hash.startsWith('gallery-')) {
    const slug = hash.replace('gallery-', '')
    selectedGallerySlug.value = slug
    currentPage.value = `gallery-${slug}`
  } else if (hash === 'portfolio' || hash === 'services' || hash === 'home') {
    currentPage.value = hash
    selectedGallerySlug.value = ''
  } else {
    currentPage.value = 'home'
    selectedGallerySlug.value = ''
  }
}

const navigateTo = (page: string) => {
  currentPage.value = page
  if (page.startsWith('gallery-')) {
    const slug = page.replace('gallery-', '')
    selectedGallerySlug.value = slug
    window.location.hash = `gallery-${slug}`
  } else {
    selectedGallerySlug.value = ''
    window.location.hash = page
  }
  window.scrollTo({ top: 0, behavior: isMobile() ? 'auto' : 'smooth' })
}

const openGalleryFromHome = (slug: string) => {
  navigateTo(`gallery-${slug}`)
}

const closeGallery = () => {
  navigateTo('portfolio')
}

const services = [
  {
    slug: 'ritratti-professionali',
    title: 'Sessioni di Ritratto',
    details: 'Ritratti in studio e on location per professionisti, team e creativi.',
    eyebrow: 'Ritratti professionali',
    pageTitle: 'Ritratti professionali per team, founder e creativi',
    summary: 'Sessioni pensate per costruire una presenza visiva riconoscibile, adatta a siti, profili social, press kit e comunicazione aziendale.',
    image: 'https://images.unsplash.com/photo-1544723795-3fb6469f5b39?auto=format&fit=crop&w=1400&q=82',
    highlights: ['Direzione posa naturale', 'Scatti in studio o on location', 'Selezione ottimizzata per web e social'],
    deliverables: ['Ritratti individuali', 'Foto team', 'Immagini profilo e press kit'],
  },
  {
    slug: 'eventi-aziendali-locali',
    title: 'Fotografia per Eventi',
    details: 'Copertura elegante per aziende, attività e locali, con servizi per inaugurazioni, serate e lanci commerciali.',
    eyebrow: 'Eventi aziendali e locali',
    pageTitle: 'Fotografia per eventi aziendali, inaugurazioni e serate nei locali',
    summary: 'Reportage dinamici per raccontare atmosfera, partecipazione, dettagli e identità del tuo evento senza pose forzate.',
    image: 'https://images.unsplash.com/photo-1511578314322-379afb476865?auto=format&fit=crop&w=1400&q=82',
    highlights: ['Racconto spontaneo dell’evento', 'Dettagli del venue e del brand', 'Consegna rapida per comunicazione post-evento'],
    deliverables: ['Gallery evento', 'Selezione social', 'Scatti per comunicati e campagne'],
  },
  {
    slug: 'fotografia-commerciale-brand',
    title: 'Lavoro Commerciale',
    details: 'Storytelling del brand, immagini editoriali e campagne creative.',
    eyebrow: 'Fotografia commerciale',
    pageTitle: 'Fotografia commerciale per brand, attività e campagne creative',
    summary: 'Immagini curate per raccontare prodotti, ambienti, persone e valori del brand con un taglio editoriale e contemporaneo.',
    image: 'https://images.unsplash.com/photo-1556742502-ec7c0e9f34b1?auto=format&fit=crop&w=1400&q=82',
    highlights: ['Moodboard e direzione creativa', 'Scatti per sito, ADV e social', 'Coerenza visiva con identità del brand'],
    deliverables: ['Campagne visual', 'Foto prodotto ambientate', 'Contenuti per sito e social'],
  },
]

const particles = () => {
  const allParticles = [
    { x: 7, y: 14, size: 7, color: 'cyan', drift: 28, delay: '0s' },
    { x: 18, y: 38, size: 4, color: 'pink', drift: -34, delay: '-1.4s' },
    { x: 32, y: 24, size: 5, color: 'orange', drift: 22, delay: '-2.2s' },
    { x: 47, y: 58, size: 8, color: 'cyan', drift: -26, delay: '-0.8s' },
    { x: 63, y: 18, size: 4, color: 'pink', drift: 32, delay: '-3s' },
    { x: 78, y: 44, size: 6, color: 'orange', drift: -22, delay: '-1.8s' },
    { x: 88, y: 70, size: 5, color: 'cyan', drift: 30, delay: '-2.7s' },
    { x: 12, y: 76, size: 9, color: 'pink', drift: -28, delay: '-0.4s' },
    { x: 38, y: 84, size: 4, color: 'orange', drift: 26, delay: '-3.5s' },
    { x: 57, y: 73, size: 7, color: 'cyan', drift: -30, delay: '-1.1s' },
    { x: 72, y: 88, size: 4, color: 'pink', drift: 24, delay: '-2.9s' },
    { x: 94, y: 28, size: 8, color: 'orange', drift: -32, delay: '-1.7s' },
  ]
  
  if (typeof window !== 'undefined' && window.innerWidth <= 768) {
    return allParticles.slice(0, 2) // Solo 2 particelle su mobile
  }
  return allParticles
}

const selectedServiceSlug = ref('')

let frame = 0

const isMobile = () => window.innerWidth <= 768

const updateScrollEffects = () => {
  frame = 0
  if (!isMobile()) {
    document.documentElement.style.setProperty('--scroll-shift', `${window.scrollY * 0.08}px`)
  }
}

const onScroll = () => {
  if (!frame && !isMobile()) {
    frame = window.requestAnimationFrame(updateScrollEffects)
  }
}

onMounted(() => {
  syncRouteFromHash()
  updateScrollEffects()
  if (!isMobile()) {
    window.addEventListener('scroll', onScroll, { passive: true })
  }
  window.addEventListener('hashchange', syncRouteFromHash)
})

onUnmounted(() => {
  if (frame) {
    window.cancelAnimationFrame(frame)
  }
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('hashchange', syncRouteFromHash)
})
</script>

<template>
  <div class="app-shell">
    <Navigation :current-page="currentPage" @navigate="navigateTo" />
    
    <div class="page-wrapper">
      <HomePage
        v-if="currentPage === 'home'"
        key="home"
        :gallery-items="galleryItems"
        :services="services"
        :particles="particles()"
        @open-gallery="openGalleryFromHome"
        @open-service="(slug) => { selectedServiceSlug = slug }"
      />
      
      <GalleryPage
        v-else-if="currentPage.startsWith('gallery-') && selectedGallery"
        :gallery="selectedGallery"
        @back="closeGallery"
      />

      <div v-else class="page-placeholder">
        <p>Pagina in costruzione</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-shell {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.page-wrapper {
  flex: 1;
}

.page-placeholder {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  color: var(--text-muted);
}
</style>
