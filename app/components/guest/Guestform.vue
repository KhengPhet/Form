<script setup>
const guestName = ref("ភ្ញៀវកិត្តិយស");
const attendance = ref("yes");
const guestCount = ref(1);

// Countdown Logic
const timeLeft = ref({ days: "00", hours: "00", mins: "00", secs: "00" });
onMounted(() => {
  const targetDate = new Date("2026-02-12T16:30:00").getTime();

  setInterval(() => {
    const now = new Date().getTime();
    const distance = targetDate - now;

    timeLeft.value = {
      days: Math.floor(distance / (1000 * 60 * 60 * 24))
        .toString()
        .padStart(2, "0"),
      hours: Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
        .toString()
        .padStart(2, "0"),
      mins: Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
        .toString()
        .padStart(2, "0"),
      secs: Math.floor((distance % (1000 * 60)) / 1000)
        .toString()
        .padStart(2, "0"),
    };
  }, 1000);
});
</script>

<template>
  <div class="silk-texture relative min-h-screen">
    <div class="romduol-corner top-0 left-0"></div>
    <div class="romduol-corner top-0 right-0 -scale-x-100"></div>

    <header>
      <div class="relative z-10 text-center px-6">
        <!-- Hero Section -->
        <section
          class="relative flex items-center justify-center bg-cover bg-center relative min-h-[700px] flex flex-col items-center justify-center text-center px-6 rounded-3xl overflow-hidden shadow-2xl"
          style="background-image: url(&quot;/banner_image.png&quot;)"
        >
          <!-- Overlay -->
          <div class="absolute inset-0 bg-black/40"></div>

          <!-- Content -->
          <div class="relative text-center px-6">
            <!-- Subtitle -->
            <p
              class="font-moul text-2xl tracking-widest text-[#F7E7B3] mb-6 drop-shadow-lg"
            >
              សិរីសួស្តី អាពាហ៍ពិពាហ៍
            </p>

            <!-- Names -->
            <h1
              class="text-4xl md:text-7xl font-black text-white leading-[1.3] tracking-tight konkhmer-sleokchher-regular"
            >
              <br /><span class="text-primary italic text-yellow-500"
                >ភា និង ស្រីល័ក្ខ</span
              >
            </h1>

            <!-- Heart Divider -->
            <div
              class="flex items-center justify-center gap-6 text-[#EBC410] mb-14"
            >
              <span class="w-24 h-px bg-[#EBC410]/70"></span>
              <span class="text-xl">♥</span>
              <span class="w-24 h-px bg-[#EBC410]/70"></span>
            </div>

            <!-- Countdown -->
            <div class="flex justify-center gap-4 flex-wrap">
              <div
                v-for="(val, unit) in timeLeft"
                :key="unit"
                class="flex flex-col items-center justify-center w-20 h-24 rounded-xl border border-primary/40 bg-white/30 backdrop-blur-md"
              >
                <span class="text-2xl font-bold text-primary">
                  {{ val }}
                </span>
                <span
                  class="text-[10px] uppercase font-bold tracking-widest text-charcoal/80"
                >
                  {{
                    unit === "days"
                      ? "ថ្ងៃ"
                      : unit === "hours"
                        ? "ម៉ោង"
                        : unit === "mins"
                          ? "នាទី"
                          : "វិនាទី"
                  }}
                </span>
              </div>
            </div>
          </div>
        </section>
      </div>
    </header>
    <section class="py-32 px-6">
      <div class="max-w-6xl mx-auto text-center">
        <!-- title -->
        <h2
          class="font-moul text-4xl text-royal-blue mb-6 text-[#C9A63A] from-[#C9A63A] to-[#E6C56E]"
        >
          កម្មវិធីពិសាភោជនាហារ
        </h2>
        <!-- ornament -->
        <div class="flex items-center justify-center gap-6 ">
          <span class="w-24 h-px bg-primary/40"></span>
          <span class="w-6 h-6 bg-primary/40 rotate-45"></span>
          <span class="w-24 h-px bg-primary/40"></span>
        </div>

        <!-- details -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-20 mb-24">
          <div v-for="item in details" :key="item.title" class="space-y-6">
            <!-- icon -->
            <div class="flex justify-center">
              <span
                class="material-symbols-outlined text-[3rem]"
                :style="{ color: '#C9A63A' }"
              >
                {{ item.icon }}
              </span>
            </div>

            <!-- title -->
            <h3 class="font-moul text-2xl" :style="{ color: '#C9A63A' }">
              {{ item.title }}
            </h3>

            <!-- desc -->
            <p class="text-charcoal/80 leading-relaxed" v-html="item.desc"></p>
          </div>
        </div>

        <!-- button -->
        <div class="flex justify-center">
          <button
            type="submit"
            class="py-4 bg-gradient-to-r from-[#C9A63A] to-[#E6C56E] text-white font-moul text-lg shadow-lg hover:scale-[1.02] transition flex items-center gap-2 px-6 rounded-lg"
          >
            <span class="material-symbols-outlined">near_me</span>
            មើលទីតាំងលើផែនទី
          </button>
        </div>
      </div>
    </section>

    <section class="flex items-center justify-center px-4">
      <form
        @submit.prevent="handleSubmit"
        class="relative w-full max-w-3xl bg-white border border-[#E8D8A8] p-10 md:p-14 shadow-xl"
      >
        <!-- corner ornaments -->
        <span
          class="absolute top-3 left-3 w-4 h-4 bg-[#E8D8A8] rotate-45"
        ></span>
        <span
          class="absolute top-3 right-3 w-4 h-4 bg-[#E8D8A8] rotate-45"
        ></span>
        <span
          class="absolute bottom-3 left-3 w-4 h-4 bg-[#E8D8A8] rotate-45"
        ></span>
        <span
          class="absolute bottom-3 right-3 w-4 h-4 bg-[#E8D8A8] rotate-45"
        ></span>

        <!-- title -->
        <div class="text-center mb-10">
          <p class="text-sm text-[#C9A63A] tracking-wide mb-2">
            សូមមេត្តាបញ្ជាក់ការចូលរួមក្នុងពិធីមង្គលការ
          </p>
          <h2 class="font-moul text-3xl text-[#1F3C88] mb-3">
            ការឆ្លើយតបការអញ្ជើញ
          </h2>
          <p class="text-sm text-gray-500 leading-relaxed">
            សូមបំពេញព័ត៌មានខាងក្រោម ដើម្បីឲ្យយើងខ្ញុំអាចរៀបចំបានយ៉ាងល្អប្រសើរ
          </p>
        </div>

        <!-- guest -->
        <div class="text-center border-y border-[#E8D8A8] py-4 mb-12">
          <span class="text-[#1F3C88]">ជូនចំពោះ៖ </span>
          <span class="font-moul text-xl text-[#C9A63A]">
            {{ guestName || "ភ្ញៀវកិត្តិយស" }}
          </span>
        </div>

        <!-- attend -->
        <div class="text-center mb-12">
          <p class="text-sm text-[#C9A63A] mb-6">
            តើលោក/លោកស្រី នឹងអញ្ជើញចូលរួមទេ?
          </p>

          <div class="flex justify-center gap-10">
            <label class="flex items-center gap-3 cursor-pointer">
              <input
                type="radio"
                value="yes"
                v-model="attend"
                class="w-5 h-5 accent-[#C9A63A]"
              />
              <span class="text-gray-700">ចូលរួម</span>
            </label>

            <label class="flex items-center gap-3 cursor-pointer">
              <input
                type="radio"
                value="no"
                v-model="attend"
                class="w-5 h-5 accent-[#C9A63A]"
              />
              <span class="text-gray-700">មិនអាចចូលរួម</span>
            </label>
          </div>
        </div>

        <!-- inputs -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-12">
          <div>
            <label class="flex items-center gap-2 text-xs text-[#C9A63A] mb-2">
              <span>👤</span>
              ឈ្មោះភ្ញៀវកិត្តិយស
            </label>
            <input
              v-model="guestName"
              type="text"
              placeholder="សូមបញ្ចូលឈ្មោះ"
              class="w-full bg-transparent border-0 border-b border-[#E8D8A8] focus:border-[#C9A63A] focus:ring-0 py-2 outline-none"
            />
          </div>

          <div>
            <label class="flex items-center gap-2 text-xs text-[#C9A63A] mb-2">
              <span>👥</span>
              ចំនួនភ្ញៀវ (មនុស្ស)
            </label>
            <input
              v-model="guestCount"
              type="number"
              min="1"
              class="w-full bg-transparent border-0 border-b border-[#E8D8A8] focus:border-[#C9A63A] focus:ring-0 py-2 outline-none"
            />
          </div>
        </div>

        <!-- submit -->
        <button
          type="submit"
          class="w-full py-4 bg-gradient-to-r from-[#C9A63A] to-[#E6C56E] text-white font-moul text-lg shadow-lg hover:scale-[1.02] transition"
        >
          បញ្ជូនការឆ្លើយតប
        </button>
      </form>
    </section>
  </div>
</template>

<script>
import { ref } from "vue";

const guestName = ref("");
const guestCount = ref(1);
const attend = ref("yes");

const handleSubmit = () => {
  const payload = {
    name: guestName.value,
    count: guestCount.value,
    attend: attend.value,
  };

  console.log(payload);
  // send to Supabase / API here
};
const details = [
  {
    title: "កាលបរិច្ឆេទ",
    icon: "calendar_today",
    desc: "ថ្ងៃព្រហស្បត្តិ៍ ទី១២ ខែកុម្ភៈ ឆ្នាំ២០២៦ <br/> <small> </small>",
  },
  {
    title: "ម៉ោងពេល",
    icon: "history_toggle_off",
    desc: "ចាប់ផ្ដើមទទួលភ្ញៀវ <br/> <strong>០៥​:៣០ ល្ងាច</strong>",
  },
  {
    title: "ទីតាំង",
    icon: "distance",
    desc: "ភូមិ នាងទើត​​ ឃុំ នាងទើត  <br/> ស្រុកតំបែរ",
  },
];
</script>
