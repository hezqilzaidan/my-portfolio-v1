<script>
export default {
  name: 'EventView',
  data() {
    return {
      events: [
        {
          id: 1,
          name: 'Google Devfest Depok 2024',
          date: '2024',
          location: 'Depok, Indonesia',
          description: 'Konferensi teknologi tahunan Google Developer Group yang menghadirkan sesi teknis, workshop, dan networking dengan developer lokal.',
          photos: [
            '/img3/dvd1.jpg',
            '/img3/dvd2.jpg',
            '/img3/dvd3.jpg'
          ],
          category: 'tech-conference'
        },
        {
          id: 2,
          name: 'Google Devfest Jakarta 2024',
          date: '2024',
          location: 'Jakarta, Indonesia',
          description: 'Event teknologi terbesar di Jakarta yang mempertemukan developer, designer, dan tech enthusiast untuk berbagi pengetahuan dan inovasi.',
          photos: [
            '/img3/dvj1.jpg',
            '/img3/dvj2.jpg'
          ],
          category: 'tech-conference'
        },
        {
          id: 3,
          name: 'Alibaba Cloud Summit 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Konferensi cloud computing yang menampilkan teknologi terbaru Alibaba Cloud, best practices, dan roadmap pengembangan cloud di Indonesia.',
          photos: [
            '/img3/albs1.jpg',
            '/img3/albs2.jpg',
            '/img3/albs3.jpg'
          ],
          category: 'cloud-summit'
        },
        {
          id: 4,
          name: 'Build With AI GDG Depok 2025',
          date: '2025',
          location: 'Depok, Indonesia',
          description: 'Workshop dan seminar tentang pengembangan aplikasi menggunakan AI, machine learning, dan tools Google AI terbaru.',
          photos: [
            '/img3/bwaid1.jpg',
            '/img3/bwaid2.jpg'
          ],
          category: 'ai-workshop'
        },
        {
          id: 5,
          name: 'Build With AI GDG Jakarta 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Event AI terbesar di Jakarta yang fokus pada implementasi AI dalam pengembangan aplikasi dan solusi bisnis.',
          photos: [
            '/img3/bwaij1.jpg',
            '/img3/bwaij2.jpg',
            '/img3/bwaij3.jpg'
          ],
          category: 'ai-workshop'
        },
        {
          id: 6,
          name: 'Grab Tech Talk 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Tech talk yang menghadirkan engineer dan tech leader dari Grab untuk berbagi pengalaman dan teknologi yang digunakan.',
          photos: [
            '/img3/gt1.jpg',
            '/img3/gt2.jpg',
            '/img3/gt3.jpg'
          ],
          category: 'tech-talk'
        },
        {
          id: 7,
          name: 'Google I/O Extended Bogor 2025',
          date: '2025',
          location: 'Bogor, Indonesia',
          description: 'Extended event dari Google I/O yang menampilkan teknologi terbaru Google, Android, Flutter, dan Firebase.',
          photos: [
            '/img3/giob1.jpg',
            '/img3/giob2.jpg',
            '/img3/giob3.jpg'
          ],
          category: 'google-io'
        },
        {
          id: 8,
          name: 'Google I/O Extended Jakarta 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Event Google I/O terbesar di Indonesia yang menghadirkan sesi teknis, demo produk, dan networking dengan Google Developer Experts.',
          photos: [
            '/img3/gioj1.jpg',
            '/img3/gioj2.jpg',
            '/img3/gioj3.jpg'
          ],
          category: 'google-io'
        },
        {
          id: 9,
          name: 'AWS Summit Jakarta 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Konferensi AWS terbesar di Indonesia yang menampilkan layanan cloud terbaru, best practices, dan customer success stories.',
          photos: [
            '/img3/aws1.jpg',
            '/img3/aws2.jpg',
            '/img3/aws3.jpg',
            '/img3/aws4.jpg',
            '/img3/aws5.jpg'
          ],
          category: 'aws-summit'
        },
        {
          id: 10,
          name: 'AWS x Datadog 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Kolaborasi AWS dan Datadog untuk monitoring dan observability cloud, menampilkan integrasi dan best practices monitoring.',
          photos: [
            '/img3/dtdog1.jpg',
            '/img3/dtdog2.jpg',
            '/img3/dtdog3.jpg'
          ],
          category: 'aws-summit'
        },
        {
          id: 11,
          name: 'Alibaba Cloud x MongoDB 2025',
          date: '2025',
          location: 'Jakarta, Indonesia',
          description: 'Event kolaborasi Alibaba Cloud dan MongoDB yang menampilkan integrasi database NoSQL dengan cloud computing, best practices, dan use cases untuk aplikasi modern.',
          photos: [
            '/img3/albmd1.jpg',
            '/img3/albmd2.jpg',
            '/img3/albmd3.jpg'
          ],
          category: 'cloud-summit'
        }
      ],
      activeFilter: 'all',
      selectedEvent: null,
      currentPhotoIndex: 0
    };
  },
  computed: {
    filteredEvents() {
      if (this.activeFilter === 'all') return this.events;
      return this.events.filter((event) => event.category === this.activeFilter);
    }
  },
  mounted() {
    // Ensure body scroll is restored when component is mounted
    document.body.classList.remove('modal-open');
  },
  beforeUnmount() {
    // Ensure body scroll is restored when component is unmounted
    document.body.classList.remove('modal-open');
  },
  methods: {
    setFilter(filterKey) {
      this.activeFilter = filterKey;
    },
    openEventModal(event) {
      this.selectedEvent = event;
      this.currentPhotoIndex = 0;
      // Prevent body scroll when modal is open
      document.body.classList.add('modal-open');
    },
    closeEventModal() {
      this.selectedEvent = null;
      this.currentPhotoIndex = 0;
      // Restore body scroll when modal is closed
      document.body.classList.remove('modal-open');
    },
    nextPhoto() {
      if (this.selectedEvent) {
        this.currentPhotoIndex = (this.currentPhotoIndex + 1) % this.selectedEvent.photos.length;
      }
    },
    prevPhoto() {
      if (this.selectedEvent) {
        this.currentPhotoIndex = this.currentPhotoIndex === 0 
          ? this.selectedEvent.photos.length - 1 
          : this.currentPhotoIndex - 1;
      }
    },
    goToPhoto(index) {
      this.currentPhotoIndex = index;
    }
  }
};
</script>

<template>
  <div class="px-5 py-5 md:px-12 md:py-10 text-left text-amber-50 mx-3">
    <article data-page="events">
      <header>
        <div class="text-2xl font-bold text-white mb-6 fadein-bot title-section flex items-center">
          <div class="h-[1px] w-10 bg-amber-200 md:w-20"></div>
          &nbsp; Events & Conferences
        </div>
      </header>

      <section class="mb-6">
        <div class="flex flex-wrap gap-2 text-sm">
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'all', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'all' }"
            @click="setFilter('all')"
          >Semua Event</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'tech-conference', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'tech-conference' }"
            @click="setFilter('tech-conference')"
          >Tech Conference</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'ai-workshop', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'ai-workshop' }"
            @click="setFilter('ai-workshop')"
          >AI Workshop</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'aws-summit', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'aws-summit' }"
            @click="setFilter('aws-summit')"
          >AWS Summit</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'google-io', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'google-io' }"
            @click="setFilter('google-io')"
          >Google I/O</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'tech-talk', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'tech-talk' }"
            @click="setFilter('tech-talk')"
          >Tech Talk</button>
        </div>
      </section>

      <section>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div
            v-for="event in filteredEvents"
            :key="event.id"
            class="relative bg-[#1e1e1f] border border-[#383838] rounded-2xl p-5 text-amber-50 shadow-[0_0_20px_-8px_rgba(255,219,112,0.15)] hover:shadow-[0_0_30px_-8px_rgba(255,219,112,0.25)] transition-all duration-300 cursor-pointer group"
            @click="openEventModal(event)"
          >
            <div class="mb-4">
              <div class="text-white text-lg font-semibold mb-2 group-hover:text-amber-200 transition-colors">{{ event.name }}</div>
              <div class="text-amber-200 text-sm mb-2">{{ event.date }} · {{ event.location }}</div>
              <div class="text-[#cfcfcf] text-sm leading-relaxed">{{ event.description }}</div>
            </div>
            
            <div class="flex justify-between items-center">
              <div class="text-xs text-gray-400">
                Klik untuk lihat foto
              </div>
              <div class="w-8 h-8 bg-amber-200/20 rounded-full flex items-center justify-center group-hover:bg-amber-200/30 transition-colors">
                <svg class="w-4 h-4 text-amber-200" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                </svg>
              </div>
            </div>
          </div>
        </div>
      </section>
    </article>

    <!-- Event Modal -->
    <div v-if="selectedEvent" class="fixed inset-0 bg-black bg-opacity-80 z-[9999] flex items-start justify-center pt-20 p-4" @click="closeEventModal">
      <div class="bg-[#1e1e1f] border border-[#383838] rounded-2xl max-w-4xl w-full max-h-[80vh] overflow-y-auto modal-content" @click.stop>
        <div class="p-6">
          <div class="flex justify-between items-start mb-4">
            <div>
              <h2 class="text-2xl font-bold text-white mb-2">{{ selectedEvent.name }}</h2>
              <p class="text-amber-200 text-lg">{{ selectedEvent.date }} · {{ selectedEvent.location }}</p>
            </div>
            <button @click="closeEventModal" class="text-gray-400 hover:text-white transition-colors">
              <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
              </svg>
            </button>
          </div>
          
          <p class="text-[#cfcfcf] text-base leading-relaxed mb-6">{{ selectedEvent.description }}</p>
          
          <!-- Photo Gallery -->
          <div class="relative">
            <div class="relative aspect-[3/4] bg-[#2a2a2a] rounded-xl overflow-hidden mb-4">
              <img 
                :src="selectedEvent.photos[currentPhotoIndex]" 
                :alt="`${selectedEvent.name} - Photo ${currentPhotoIndex + 1}`"
                class="w-full h-full object-cover"
                @error="$event.target.src = '/img/portfolio-default.jpg'"
              />
              
              <!-- Navigation Arrows -->
              <button 
                @click="prevPhoto" 
                class="absolute left-4 top-1/2 -translate-y-1/2 w-10 h-10 bg-black bg-opacity-50 rounded-full flex items-center justify-center text-white hover:bg-opacity-70 transition-all"
              >
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
                </svg>
              </button>
              
              <button 
                @click="nextPhoto" 
                class="absolute right-4 top-1/2 -translate-y-1/2 w-10 h-10 bg-black bg-opacity-50 rounded-full flex items-center justify-center text-white hover:bg-opacity-70 transition-all"
              >
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
                </svg>
              </button>
            </div>
            
            <!-- Photo Indicators -->
            <div class="flex justify-center gap-2 mb-4">
              <button
                v-for="(photo, index) in selectedEvent.photos"
                :key="index"
                @click="goToPhoto(index)"
                class="w-3 h-3 rounded-full transition-all"
                :class="index === currentPhotoIndex ? 'bg-amber-200' : 'bg-gray-500 hover:bg-gray-400'"
              ></button>
            </div>
            
            <!-- Photo Counter -->
            <div class="text-center text-sm text-gray-400">
              {{ currentPhotoIndex + 1 }} / {{ selectedEvent.photos.length }}
            </div>
          </div>
          
          <!-- Instructions -->
          <div class="mt-6 p-4 bg-[#2a2a2a] rounded-lg border border-[#383838]">
            <div class="flex items-center gap-2 text-amber-200 mb-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
              </svg>
              <span class="font-semibold">Cara Navigasi</span>
            </div>
            <div class="text-sm text-[#cfcfcf] space-y-1">
              <p>• Klik tombol panah kiri/kanan untuk melihat foto berikutnya</p>
              <p>• Klik indikator bulat untuk langsung ke foto tertentu</p>
              <p>• Geser dengan mouse atau touch untuk navigasi</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fadein-bot {
  opacity: 0;
  animation: fadeInBot 0.5s forwards;
}

@keyframes fadeInBot {
  from {
    opacity: 0;
    transform: translate3d(0, -100%, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

/* Smooth transitions for modal */
.modal-enter-active, .modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from, .modal-leave-to {
  opacity: 0;
}

/* Hover effects for cards */
.group:hover {
  transform: translateY(-2px);
}

/* Custom scrollbar for modal */
.overflow-y-auto::-webkit-scrollbar {
  width: 6px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: #2a2a2a;
  border-radius: 3px;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background: #ffdb70;
  border-radius: 3px;
}

.overflow-y-auto::-webkit-scrollbar-thumb:hover {
  background: #ffd54f;
}

/* Ensure modal is always on top */
.fixed.inset-0 {
  z-index: 9999 !important;
}

/* Modal positioning and scroll behavior */
.modal-content {
  max-height: calc(100vh - 120px);
  overflow-y: auto;
  scrollbar-width: thin;
  scrollbar-color: #ffdb70 #2a2a2a;
}

/* Prevent body scroll when modal is open */
body.modal-open {
  overflow: hidden;
}
</style>
