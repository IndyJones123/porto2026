<script setup lang="ts">
const stats = [
    { number: '3+', label: 'Years Experience' },
    { number: '7+', label: 'Project Finished' },
    { number: 'S1', label: 'Computer Science' },
    { number: '3.9', label: 'GPA Score', sub: '/4.0' },
];
</script>

<template>
    <section class="py-20 bg-bg-secondary px-[5%]">
        <div class="max-w-[1200px] mx-auto grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
            <div v-for="stat in stats" :key="stat.label" class="text-center p-8 bg-bg-card/30 rounded-xl hover:bg-bg-card transition-colors duration-300">
                <div class="text-4xl lg:text-5xl font-bold text-accent-blue mb-2">
                    {{ stat.number }}<span v-if="stat.sub" class="text-2xl text-text-secondary">{{ stat.sub }}</span>
                </div>
                <div class="text-text-secondary text-lg">{{ stat.label }}</div>
            </div>
        </div>
    </section>
</template>
