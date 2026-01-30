<script setup lang="ts">
import { reactive, ref } from 'vue'

/* =====================
  State
===================== */
const form = reactive({
  groom: '',
  bride: '',
  phone: '',
  telegram: '',
  date: '',
  location: '',
  traditional: 1,
  modern: 1,
  color: 'gold',
  images: [] as File[]
})

/* =====================
  File Upload
===================== */
const fileInput = ref<HTMLInputElement | null>(null)

const openFilePicker = () => {
  fileInput.value?.click()
}

const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement
  if (!target.files) return
  form.images = Array.from(target.files)
}

/* =====================
  Submit
===================== */
const submitForm = () => {
  const payload = {
    ...form,
    imageCount: form.images.length
  }

  console.log('SUBMIT 👉', payload)

  // example API
  // await $fetch('/api/booking', { method: 'POST', body: payload })
}
</script>

<template>
  <div class="min-h-screen bg-bgLight text-gray-800">

    <!-- Background -->
    <div class="fixed inset-0 -z-10 overflow-hidden">
      <div class="absolute -top-24 -right-24 h-96 w-96 rounded-full bg-primary/10 blur-3xl" />
      <div class="absolute top-1/2 -left-24 h-80 w-80 rounded-full bg-accent/10 blur-3xl" />
    </div>

    <main class="mx-auto max-w-md px-4 py-8 pb-24">

      <!-- Header -->
      <header class="mb-8 text-center">
        <span class="material-icons-outlined block text-4xl text-primary">
          spa
        </span>
        <h1 class="font-moul mt-2 text-xl">
          ព័ត៌មានសម្រាប់ការថតរូប Pre-Wedding
        </h1>
        <p class="mt-1 text-xs text-gray-500">
          សូមបំពេញព័ត៌មានលម្អិតដើម្បីទទួលបានបទពិសោធន៍ល្អបំផុត
        </p>
      </header>

      <!-- Card -->
      <section class="glass rounded-2xl border border-gray-100 p-6 shadow-xl">

        <form class="space-y-8" @submit.prevent="submitForm">

          <!-- Personal -->
          <fieldset>
            <legend class="mb-4 flex items-center gap-2 text-sm font-bold">
              <span class="material-icons-outlined text-primary">person</span>
              ១. ព័ត៌មានផ្ទាល់ខ្លួន
            </legend>

            <div class="grid grid-cols-2 gap-4">
              <input v-model.trim="form.groom" placeholder="ឈ្មោះកូនកំលោះ" />
              <input v-model.trim="form.bride" placeholder="ឈ្មោះកូនក្រមុំ" />
              <input v-model.trim="form.phone" placeholder="0XX XXX XXX" />
              <input v-model.trim="form.telegram" placeholder="@telegram" />
            </div>
          </fieldset>

          <!-- Session -->
          <fieldset>
            <legend class="mb-4 flex items-center gap-2 text-sm font-bold">
              <span class="material-icons-outlined text-primary">event</span>
              ២. ការជ្រើសរើសកញ្ចប់ថត
            </legend>

            <div class="grid grid-cols-2 gap-4">
              <input type="date" v-model="form.date" />
              <select v-model="form.location">
                <option value="">-- ជ្រើសរើស --</option>
                <option>ប្រាសាទបុរាណ</option>
                <option>មាត់សមុទ្រ</option>
                <option>Studio</option>
              </select>
            </div>
          </fieldset>

          <!-- Outfit -->
          <fieldset>
            <legend class="mb-4 flex items-center gap-2 text-sm font-bold">
              <span class="material-icons-outlined text-primary">style</span>
              ៣. Outfit & Style
            </legend>

            <div class="mb-4 grid grid-cols-2 gap-4">
              <input type="number" min="0" v-model.number="form.traditional" />
              <input type="number" min="0" v-model.number="form.modern" />
            </div>

            <div class="flex gap-4 text-xs">
              <label class="flex cursor-pointer items-center gap-2">
                <input type="radio" value="gold" v-model="form.color" />
                <span class="flex items-center gap-1">
                  <span class="h-3 w-3 rounded-full bg-primary" /> Gold
                </span>
              </label>

              <label class="flex cursor-pointer items-center gap-2">
                <input type="radio" value="blue" v-model="form.color" />
                <span class="flex items-center gap-1">
                  <span class="h-3 w-3 rounded-full bg-blue-500" /> Blue
                </span>
              </label>
            </div>
          </fieldset>

          <!-- Upload -->
          <fieldset>
            <legend class="mb-4 flex items-center gap-2 text-sm font-bold">
              <span class="material-icons-outlined text-primary">collections</span>
              ៤. Image Upload
            </legend>

            <div
              class="cursor-pointer rounded-xl border-2 border-dashed border-primary/30 bg-primary/5 p-8 text-center"
              @click="openFilePicker"
            >
              <span class="material-icons-outlined mb-2 text-3xl text-primary">
                add_photo_alternate
              </span>

              <p class="text-xs">
                ទម្លាក់រូប ឬ Moodboard របស់អ្នកនៅទីនេះ
              </p>

              <p v-if="form.images.length" class="mt-1 text-[10px] text-gray-500">
                📸 {{ form.images.length }} file(s) selected
              </p>

              <input
                ref="fileInput"
                type="file"
                class="hidden"
                multiple
                accept="image/*"
                @change="handleFileChange"
              />
            </div>
          </fieldset>

          <!-- Actions -->
          <div class="flex gap-4">
            <button
              type="button"
              class="flex-1 rounded-xl border border-primary/30 py-3 font-bold text-primary"
            >
              ត្រឡប់ក្រោយ
            </button>

            <button
              type="submit"
              class="flex-[1.5] rounded-xl bg-primary py-3 font-bold text-white"
            >
              បន្ទាប់ →
            </button>
          </div>

        </form>
      </section>
    </main>

    <!-- Bottom Nav -->
    <nav class="fixed bottom-0 left-0 right-0 flex justify-around border-t bg-white/90 py-3 text-[8px] font-bold backdrop-blur">
      <div class="flex flex-col items-center opacity-40">
        <span class="material-icons-outlined">home</span>ទំព័រដើម
      </div>
      <div class="flex flex-col items-center text-primary">
        <span class="material-icons-outlined">event</span>កក់ទុក
      </div>
      <div class="flex flex-col items-center opacity-40">
        <span class="material-icons-outlined">photo_library</span>ស្នាដៃ
      </div>
      <div class="flex flex-col items-center opacity-40">
        <span class="material-icons-outlined">person_outline</span>គណនី
      </div>
    </nav>

  </div>
</template>
