<script setup lang="ts">
import Timeline from 'primevue/timeline';

const events = [
    { 
        year: '2025 - Present', 
        title: 'Senior Software Engineer', 
        company: 'OG x AOR', 
        desc: 'Focusing on developing a marketplace website system across game servers using FastAPI and optimizing the frontend with React for high-performance delivery.' 
    },
    { 
        year: '2024 - Present', 
        title: 'Junior Software Engineer', 
        company: 'Mitrasoft Global Perdana', 
        desc: 'Building various surrounding applications for Sharia core banking and create a custom project for large-scale enterprise clients.' 
    },
    { 
        year: '2023', 
        title: 'Junior Developer / Intern', 
        company: 'PT. Agrofarm Nusa Raya', 
        desc: 'Developed the PT. Agrofarm Nusa Raya landing page and a web-based attendance management system using Laravel.' 
    },
];
</script>

<template>
    <section class="py-24 px-[5%]" id="experience">
        <div class="max-w-[800px] mx-auto">
            <div class="text-center mb-16">
                <span class="text-accent-blue font-semibold uppercase tracking-widest text-sm mb-4 block">Career Path</span>
                <h2 class="text-3xl md:text-5xl font-bold">Work Experience</h2>
            </div>
            
            <Timeline :value="events" align="alternate" class="customized-timeline">
                <template #content="slotProps">
                    <div class="bg-bg-card p-6 rounded-xl border border-accent-blue/10 hover:border-accent-blue transition-colors duration-300 shadow-xl mb-10">
                        <h3 class="text-xl font-bold text-white mb-1">{{ slotProps.item.title }}</h3>
                        <span class="text-accent-blue text-sm italic mb-4 block">{{ slotProps.item.company }}</span>
                        <p class="text-text-secondary text-sm leading-relaxed" v-html="slotProps.item.desc.replace('FastAPI', '<b>FastAPI</b>').replace('React', '<b>React</b>').replace('Laravel', '<b>Laravel</b>')"></p>
                    </div>
                </template>
                <template #opposite="slotProps">
                     <span class="text-accent-blue font-extrabold text-lg">{{ slotProps.item.year }}</span>
                </template>
                <template #marker>
                    <div class="w-5 h-5 bg-bg-primary border-[3px] border-accent-blue rounded-full z-10 box-content"></div>
                </template>
            </Timeline>
        </div>
    </section>
</template>

<style scoped>
:deep(.p-timeline-event-content) {
    padding-bottom: 3rem;
}
:deep(.p-timeline-event-connector) {
    background-color: rgba(74, 158, 255, 0.2);
}
</style>
