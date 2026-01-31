<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { useRouter } from 'vue-router'

/* ================= STATE ================= */
const userMenuOpen = ref(false)
const loginOpen = ref(false)

const loginForm = ref({
  email: '',
  password: ''
})

const userMenuRef = ref<HTMLElement | null>(null)

const router = useRouter()

/* ================= DATA ================= */
const navLinks = [
  { id: 1, label: 'មើលស្នាដៃ', to: '/' },
  { id: 2, label: 'កញ្ចប់សេវាកម្ម', to: '/gallery' },
  { id: 3, label: 'លិខិតអញ្ជើញ', to: '/services' },
  { id: 4, label: 'ទំនាក់ទំនង', to: '/contact' }
]


/* ================= METHODS ================= */
const toggleUserMenu = () => {
  userMenuOpen.value = !userMenuOpen.value
}

const openLogin = () => {
  userMenuOpen.value = false
  loginOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeLogin = () => {
  loginOpen.value = false
  document.body.style.overflow = ''
}

const submitLogin = () => {
  console.log('LOGIN:', loginForm.value)
  closeLogin()
}

const handleBooking = () => {
  router.push('/booking/Bookibg')
}

/* ================= CLICK OUTSIDE ================= */
const handleClickOutside = (e: MouseEvent) => {
  if (
    userMenuOpen.value &&
    userMenuRef.value &&
    !userMenuRef.value.contains(e.target as Node)
  ) {
    userMenuOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>

<template>
  <!-- ================= HEADER ================= -->
  <header class="sticky top-0 z-50 bg-white border-b">
    <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">

      <!-- Logo -->
      <NuxtLink to="/" class="flex items-center gap-2">
        <span
          class="material-symbols-outlined text-4xl text-yellow-500"
          style="font-variation-settings:'FILL' 1"
        >
          camera
        </span>
        <div>
          <h1 class="font-black leading-none">PANHA KHMER</h1>
          <span class="text-[10px] tracking-widest opacity-70">
            បញ្ញា ខ្មែរ
          </span>
        </div>
      </NuxtLink>

      <!-- Nav -->
      <nav class="hidden lg:flex gap-6">
        <NuxtLink
          v-for="link in navLinks"
          :key="link.id"
          :to="link.to"
          class="font-semibold hover:text-yellow-500"
        >
          {{ link.label }}
        </NuxtLink>
      </nav>

      <!-- User -->
      <div class="relative flex items-center gap-3" ref="userMenuRef">

        <!-- Booking -->
        <button
          class="hidden sm:flex items-center gap-2
                 bg-gradient-to-r from-yellow-500 to-yellow-600
                 text-gray-900 px-4 py-2.5 rounded-lg
                 text-sm font-bold shadow-md"
          @click="handleBooking"
        >
          <span class="material-symbols-outlined text-base">
            calendar_month
          </span>
          ថ្ងៃរៀបការ
        </button>

        <!-- Avatar -->
        <div
          class="w-10 h-10 rounded-full border-2 border-yellow-500
                 bg-cover bg-center cursor-pointer"
          style="background-image:url('https://i.pinimg.com/1200x/36/fc/c7/36fcc767ca5725d213dca3d002e23d5a.jpg')"
          @click.stop="toggleUserMenu"
        ></div>

        <!-- Dropdown -->
        <transition name="fade">
          <div
            v-if="userMenuOpen"
            class="absolute right-0 top-12 w-44
                   bg-white rounded-xl shadow border overflow-hidden"
          >
            <button
              class="w-full text-left px-4 py-2 hover:bg-gray-100"
              @click="openLogin"
            >
              🔐 Login
            </button>

            <NuxtLink
              to="/booking/Booking"
              class="block px-4 py-2 hover:bg-gray-100"
            >
              📝 Register
            </NuxtLink>
          </div>
        </transition>
      </div>
    </div>
  </header>

  <!-- ================= LOGIN MODAL ================= -->
  <transition name="fade">
    <div
      v-if="loginOpen"
      class="fixed inset-0 z-[100]
             bg-black/50 backdrop-blur-sm
             flex items-center justify-center px-4"
      @click="closeLogin"
    >
      <div
        class="w-full max-w-md bg-white rounded-2xl
               shadow-2xl p-8 relative"
        @click.stop
      >
        <!-- Close -->
        <button
          class="absolute top-4 right-4 text-gray-400 hover:text-red-500"
          @click="closeLogin"
        >
          <span class="material-symbols-outlined">close</span>
        </button>

        <!-- Title -->
        <div class="text-center mb-6">
          <span class="material-symbols-outlined text-4xl text-yellow-500">
            lock
          </span>
          <h2 class="text-2xl font-bold mt-2">ចូលគណនី</h2>
          <p class="text-sm text-gray-500">
            សូមបញ្ចូលព័ត៌មានគណនី
          </p>
        </div>

        <!-- Form -->
        <form class="space-y-5" @submit.prevent="submitLogin">
          <div>
            <label class="text-sm font-semibold">
              អ៊ីមែល / ទូរស័ព្ទ
            </label>
            <input
              v-model="loginForm.email"
              type="text"
              class="w-full mt-2 px-4 py-3 border rounded-xl
                     focus:ring-2 focus:ring-yellow-500 outline-none"
              placeholder="example@email.com"
            />
          </div>

          <div>
            <label class="text-sm font-semibold">
              ពាក្យសម្ងាត់
            </label>
            <input
              v-model="loginForm.password"
              type="password"
              class="w-full mt-2 px-4 py-3 border rounded-xl
                     focus:ring-2 focus:ring-yellow-500 outline-none"
              placeholder="********"
            />
          </div>

          <button
            type="submit"
            class="w-full py-3 bg-gradient-to-r
                   from-yellow-500 to-yellow-600
                   text-black font-bold rounded-xl shadow-lg"
          >
            🔐 Login
          </button>

          <p class="text-center text-sm text-gray-500">
            មិនទាន់មានគណនី?
            <NuxtLink to="/register" class="text-yellow-600 font-bold">
              បង្កើតថ្មី
            </NuxtLink>
          </p>
        </form>
      </div>
    </div>
  </transition>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
