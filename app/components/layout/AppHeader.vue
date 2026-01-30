<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { useRouter } from 'vue-router'

/* ================= STATE ================= */
const userMenuOpen = ref(false)

const loginForm = ref({
  username: '',
  password: ''
})

const userMenuRef = ref<HTMLElement | null>(null)
const loginDialog = ref<HTMLDialogElement | null>(null)

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

const openLoginDialog = () => {
  userMenuOpen.value = false
  if (process.client) {
    loginDialog.value?.showModal()
  }
}

const closeLoginDialog = () => {
  loginDialog.value?.close()
}

const submitLogin = () => {
  console.log('LOGIN DATA:', loginForm.value)

  // TODO: connect API here
  closeLoginDialog()
}

const handleBooking = () => {
  router.push('/booking')
}

/* ================= CLICK OUTSIDE ================= */
const handleClickOutside = (e: MouseEvent) => {
  if (
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

        <!-- Booking button -->
        <button
          class="hidden sm:flex items-center gap-2
                 bg-gradient-to-r from-yellow-500 to-yellow-600
                 hover:from-yellow-600 hover:to-yellow-700
                 text-gray-900 px-4 py-2.5 rounded-lg
                 text-sm font-bold shadow-md transition"
          @click="handleBooking"
        >
          <span class="material-symbols-outlined text-base">
            calendar_month
          </span>
          <span>ថ្ងៃរៀបការ</span>
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
              @click="openLoginDialog"
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

  <!-- ================= LOGIN DIALOG ================= -->
  <dialog
    ref="loginDialog"
    class="rounded-[36px] p-0 backdrop:bg-black/50"
  >
    <div
      class="w-[340px] bg-gradient-to-br from-[#f6ebe4] to-[#fdf6f0]
             rounded-[36px] shadow-2xl px-7 py-9 text-center relative"
    >
      <!-- Close -->
      <button
        class="absolute top-4 right-4 text-gray-400 hover:text-red-500"
        @click="closeLoginDialog"
      >
        ✕
      </button>

      <!-- Icon -->
      <div
        class="w-12 h-12 mx-auto mb-5
               bg-yellow-400 rounded-full
               flex items-center justify-center"
      >
        🌱
      </div>

      <!-- Title -->
      <h1 class="text-xl font-bold text-gray-800">
        ចូលប្រើប្រាស់គណនី<br />របស់អ្នក
      </h1>

      <div class="w-10 h-1 bg-yellow-400 mx-auto mt-4 mb-8 rounded-full"></div>

      <!-- Form -->
      <form class="space-y-5" @submit.prevent="submitLogin">
        <div class="text-left">
          <label class="text-sm font-semibold text-gray-600">
            ឈ្មោះអ្នកប្រើ
          </label>
          <input
            v-model="loginForm.username"
            type="text"
            class="w-full mt-2 rounded-xl bg-white border
                   px-4 py-3 focus:ring-2
                   focus:ring-yellow-400 outline-none"
            placeholder="បញ្ចូលឈ្មោះអ្នកប្រើ"
          />
        </div>

        <div class="text-left">
          <label class="text-sm font-semibold text-gray-600">
            ពាក្យសម្ងាត់
          </label>
          <input
            v-model="loginForm.password"
            type="password"
            class="w-full mt-2 rounded-xl bg-white border
                   px-4 py-3 focus:ring-2
                   focus:ring-yellow-400 outline-none"
            placeholder="********"
          />
        </div>

        <button
          type="submit"
          class="w-full py-3 bg-yellow-400
                 hover:bg-yellow-500 text-gray-900
                 font-bold rounded-xl transition"
        >
          ចូលគណនី →
        </button>
      </form>

      <p class="text-sm text-gray-600 mt-6">
        មិនទាន់មានគណនី?
        <NuxtLink to="/register" class="text-yellow-600 font-bold">
          ចុះឈ្មោះថ្មី
        </NuxtLink>
      </p>
    </div>
  </dialog>
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
