<script setup lang="ts">
const skills = [
    {
        icon: '⚡',
        title: 'Frontend',
        items: ['React', 'Vue.js', 'TypeScript', 'Tailwind CSS', 'Next.js']
    },
    {
        icon: '⚙️',
        title: 'Backend',
        items: ['Python (FastAPI)', 'Laravel', 'PostgreSQL', 'MySQL']
    },
    {
        icon: '🛠️',
        title: 'Tools',
        items: ['Git', 'Docker', 'AWS', 'Figma', 'VS Code']
    }
];
</script>

<template>
    <section class="py-24 bg-bg-secondary px-[5%]" id="skills">
        <div class="max-w-[1200px] mx-auto">
             <div class="mb-16">
                 <span class="text-accent-blue font-semibold uppercase tracking-widest text-sm mb-4 block">Expertise</span>
                <h2 class="text-4xl font-bold mb-4">Skills & Tools</h2>
                <p class="text-text-secondary text-lg">Technologies I use to bring ideas to life</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div v-for="skill in skills" :key="skill.title" 
                     class="bg-bg-card p-8 rounded-xl border border-accent-blue/10 hover:border-accent-blue hover:-translate-y-2 transition-all duration-300 group">
                    <div class="text-4xl mb-6">{{ skill.icon }}</div>
                    <h3 class="text-2xl font-semibold mb-6 group-hover:text-accent-blue transition-colors">{{ skill.title }}</h3>
                    <div class="flex flex-wrap gap-2">
                        <span v-for="item in skill.items" :key="item" 
                              class="px-4 py-2 bg-accent-blue/5 rounded-md text-sm text-text-secondary group-hover:bg-accent-blue/10 group-hover:text-white transition-colors">
                            {{ item }}
                        </span>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
