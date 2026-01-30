<script setup>
import { timelines } from '~/models/mode_home/timeline.model'
</script>
<template>
    <section class="py-24 px-6 lg:px-10 bg-background-light dark:bg-background-dark overflow-hidden">
        <div class="max-w-7xl mx-auto">
            <!-- Header -->
            <div class="text-center mb-16 space-y-4">
                <div class="inline-flex items-center gap-3 text-primary mb-2">
                    <span class="material-symbols-outlined text-xl">psychiatry</span>
                    <span class="text-xs font-bold uppercase tracking-[0.3em]">
                        ការរៀបចំថ្ងៃពិសេស
                    </span>
                    <span class="material-symbols-outlined text-xl">psychiatry</span>
                </div>

                <h2 class="text-3xl md:text-5xl font-extrabold tracking-tight">
                    កាលវិភាគសម្រាប់អាពាហ៍ពិពាហ៍
                </h2>

                <div class="w-20 h-1 bg-primary mx-auto rounded-full"></div>
            </div>

            <!-- Timeline -->
            <div class="relative grid grid-cols-1 md:grid-cols-2 gap-8">
                <!-- Center Line -->
                <div class="hidden md:block absolute inset-y-0 left-1/2 -translate-x-1/2 w-[1px] bg-primary/20"></div>

                <!-- Timeline Items -->
                <div v-for="(item, index) in timelines" :key="index" class="relative group">
                    <div
                        class="bg-white dark:bg-white/5 p-8 rounded-3xl border border-champagne dark:border-white/10 shadow-sm hover:shadow-xl transition-all duration-500 hover:-translate-y-1">
                        <div class="flex items-center gap-4 mb-6">
                            <div
                                class="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center text-primary group-hover:bg-primary group-hover:text-charcoal transition-colors duration-500">
                                <span class="material-symbols-outlined text-3xl">
                                    {{ item.icon }}
                                </span>
                            </div>
                            <div>
                                <p class="text-primary font-bold text-lg">
                                    {{ item.time }}
                                </p>
                                <h3 class="text-xl font-bold">
                                    {{ item.title }}
                                </h3>
                            </div>
                        </div>

                        <div class="flex items-start gap-4 text-charcoal/60 dark:text-white/60">
                            <span class="material-symbols-outlined text-primary/60 text-lg">
                                psychiatry
                            </span>
                            <p class="text-sm leading-relaxed dark:text-black/80">
                                {{ item.description }}
                            </p>



                            
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
</template>