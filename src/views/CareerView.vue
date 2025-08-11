<script>
export default {
  name: 'CareerView',
  data() {
    return {
      activeFilter: 'all', // 'all' | 'work' | 'internship'
      experiences: [
        {
          id: 1,
          category: 'internship',
          role: 'IT Support',
          company: 'Institut STIAMI',
          period: 'Okt - Nov 2018',
          location: 'Jakarta',
          description:
            'Menangani jaringan LAN/Mikrotik, mengelola database mahasiswa, dan memelihara infrastruktur internet kampus.',
          achievements: [
            'Menangani permasalahan jaringan terkait kabel LAN dan Mikrotik.',
            'Mengelola database mahasiswa untuk memastikan konektivitas ke Wi-Fi kampus.',
            'Menyelesaikan masalah perangkat keras di fasilitas staf dan mahasiswa.',
            'Membantu tim IT dalam pemeliharaan dan pemecahan masalah infrastruktur internet kampus.'
          ],
          tech: ['Mikrotik', 'LAN', 'Database Management', 'Hardware Maintenance']
        },
        {
          id: 2,
          category: 'internship',
          role: 'Backend Developer',
          company: 'PT. Pupuk Sriwidjaja',
          period: 'Agu - Des 2022',
          location: 'Palembang',
          description:
            'Mengembangkan API, mengintegrasikan data pengguna, dan mengoptimalkan basis data DAPENSRI.',
          achievements: [
            'Mengikuti bootcamp pengembangan back-end dengan fokus pada manajemen basis data.',
            'Menghubungkan dan mengelola data pengguna di dalam basis data aplikasi.',
            'Mengintegrasikan API provinsi di Indonesia ke dalam fungsionalitas website.',
            'Memelihara dan mengoptimalkan basis data pengguna DAPENSRI.',
            'Mengembangkan dan mengimplementasikan fitur baru untuk aplikasi web DAPENSRI.',
            'Menerapkan komunikasi kerja yang efektif dan kolaborasi tim.'
          ],
          tech: ['Laravel', 'MySQL', 'REST API', 'Team Collaboration']
        },
        {
          id: 3,
          category: 'work',
          role: 'Asisten Praktikum Laboratorium Informatika',
          company: 'Universitas Ahmad Dahlan',
          period: 'Mei - Juli 2023',
          location: 'Yogyakarta',
          description:
            'Mendampingi praktikum web & multimedia, mengajarkan Laravel, Photoshop, dan Blender.',
          achievements: [
            'Mendukung pelaksanaan praktikum Rekayasa Web dan Teknologi Multimedia.',
            'Mengajarkan konsep dasar framework Laravel, Adobe Photoshop, dan Blender.',
            'Memberikan bimbingan pada studi kasus pemrograman web dan desain, membantu mahasiswa mengatasi tantangan teknis.'
          ],
          tech: ['Laravel', 'HTML/CSS', 'Adobe Photoshop', 'Blender']
        },
        {
          id: 4,
          category: 'work',
          role: 'IT Staff',
          company: 'CV. Rafi Creative Collection',
          period: 'Jan - Des 2024',
          location: 'Bekasi',
          description:
            'Mengelola website profil, data pelanggan, dan konten media sosial perusahaan.',
          achievements: [
            'Mengembangkan dan memelihara website profil perusahaan.',
            'Mengelola data pelanggan dalam aplikasi internal.',
            'Mendesain dan mengawasi konten untuk media sosial perusahaan.'
          ],
          tech: ['WordPress', 'MySQL', 'Canva', 'Social Media Management']
        },
        {
          id: 5,
          category: 'work',
          role: 'Curicullum Developer',
          company: 'LeixCode',
          period: 'Juli 2024 - Present',
          location: 'Bekasi',
          description:
            'Membangun website profil, mengelola data, dan membuat konten media sosial.',
          achievements: [
            'Membangun dan memelihara website profil perusahaan.',
            'Mengatur dan memperbarui data pelanggan di sistem internal.',
            'Membuat konten visual dan tulisan untuk media sosial perusahaan.'
          ],
          tech: ['HTML', 'Tailwind CSS', 'JavaScript', 'Figma']
        }
      ]
    };
  },
  computed: {
    filteredExperiences() {
      if (this.activeFilter === 'all') return this.experiences;
      return this.experiences.filter((exp) => exp.category === this.activeFilter);
    }
  },
  methods: {
    setFilter(filterKey) {
      this.activeFilter = filterKey;
    }
  }
};
</script>

<template>
  <div class="px-5 py-5 md:px-12 md:py-10 text-left text-amber-50 mx-3">
    <article data-page="career">
      <header>
        <div class="text-2xl font-bold text-white mb-6 fadein-bot title-section flex items-center">
          <div class="h-[1px] w-10 bg-amber-200 md:w-20"></div>
          &nbsp; Career Experience
        </div>
      </header>

      <section class="mb-6">
        <div class="flex flex-wrap gap-2 text-sm">
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'all', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'all' }"
            @click="setFilter('all')"
          >Semua</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'work', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'work' }"
            @click="setFilter('work')"
          >Kerja</button>
          <button
            class="px-4 py-2 rounded-lg border transition duration-200 hover:text-white"
            :class="{ 'text-amber-200 border-amber-200 bg-amber-200/10': activeFilter === 'internship', 'border-[#3a3a3a] text-gray-300': activeFilter !== 'internship' }"
            @click="setFilter('internship')"
          >Magang</button>
        </div>
      </section>

      <section>
        <div class="relative">
          <div class="absolute left-4 top-0 bottom-0 w-[2px] bg-[#3a3a3a] md:left-1/2 md:-translate-x-1/2 hidden md:block"></div>
          <div class="flex flex-col gap-6">
            <div
              v-for="exp in filteredExperiences"
              :key="exp.id"
              class="relative bg-[#1e1e1f] border border-[#383838] rounded-2xl p-5 md:p-6 text-amber-50 shadow-[0_0_20px_-8px_rgba(255,219,112,0.15)]"
            >
              <div class="flex flex-col md:flex-row md:items-start md:justify-between gap-3">
                <div>
                  <div class="text-white text-lg md:text-xl font-semibold">{{ exp.role }}</div>
                  <div class="text-amber-200 text-sm md:text-base">{{ exp.company }} · <span class="capitalize">{{ exp.category }}</span></div>
                </div>
                <div class="text-xs md:text-sm text-gray-300">{{ exp.period }} · {{ exp.location }}</div>
              </div>

              <div class="mt-3 text-sm md:text-base text-[#cfcfcf]">
                {{ exp.description }}
              </div>

              <ul class="mt-3 list-disc list-inside space-y-1 text-xs md:text-sm text-[#d9d9d9]">
                <li v-for="(ach, idx) in exp.achievements" :key="idx">{{ ach }}</li>
              </ul>

              <div class="mt-4 flex flex-wrap gap-2">
                <span
                  v-for="(tech, tIdx) in exp.tech"
                  :key="tIdx"
                  class="text-xs md:text-sm px-2.5 py-1 rounded-full border border-amber-200/40 text-amber-200 bg-amber-200/10"
                >{{ tech }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>
    </article>
  </div>
</template>

<style>
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
</style>
  