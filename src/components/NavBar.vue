<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const isMenuOpen = ref(false);
const isScrolled = ref(false);
const activeSection = ref('home');

const toggleMenu = () => {
    isMenuOpen.value = !isMenuOpen.value;
    if (isMenuOpen.value) {
        document.body.style.overflow = 'hidden';
    } else {
        document.body.style.overflow = '';
    }
};

const closeMenu = () => {
    isMenuOpen.value = false;
    document.body.style.overflow = '';
};

const handleScroll = () => {
    isScrolled.value = window.scrollY > 20;
    
    // Improved active section detection
    const sections = ['home', 'experience', 'projects', 'skills', 'contact'];
    let current = 'home';
    
    for (const section of sections) {
        const el = document.getElementById(section);
        if (el) {
            const rect = el.getBoundingClientRect();
            // If the top of the section is above the middle of the screen
            if (rect.top <= 150) {
                current = section;
            }
        }
    }
    activeSection.value = current;
};

onMounted(() => {
    window.addEventListener('scroll', handleScroll);
    handleScroll(); // Initial check
});

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
});

const scrollToSection = (id: string) => {
    const element = document.getElementById(id);
    if (element) {
        const offset = 100; // Increased offset for better visibility
        const bodyRect = document.body.getBoundingClientRect().top;
        const elementRect = element.getBoundingClientRect().top;
        const elementPosition = elementRect - bodyRect;
        const offsetPosition = elementPosition - offset;

        window.scrollTo({
            top: offsetPosition,
            behavior: 'smooth'
        });
        closeMenu();
    }
};


const navLinks = [
    { name: 'Home', href: 'home' },
    { name: 'Experience', href: 'experience' },
    { name: 'Projects', href: 'projects' },
    { name: 'Skills', href: 'skills' },
    { name: 'Contact', href: 'contact' },
];
</script>

<template>
    <header :class="['fixed top-0 w-full z-50 transition-all duration-500 px-[5%]', isScrolled ? 'py-4' : 'py-8']">
        <nav :class="['max-w-[1200px] mx-auto flex justify-between items-center transition-all duration-500 px-8 rounded-2xl border', 
                     isScrolled ? 'bg-bg-primary/80 backdrop-blur-xl border-white/10 py-3 shadow-[0_10px_30px_rgba(0,0,0,0.3)]' : 'bg-transparent border-transparent py-0']">
            
            <div class="text-2xl font-black tracking-tighter cursor-pointer flex items-center gap-2 group" @click="scrollToSection('home')">
                <span class="text-accent-blue group-hover:scale-110 transition-transform duration-300">Alfian</span>
                <span class="text-white/40 group-hover:text-white transition-colors duration-300">Dev</span>
            </div>
            
            <!-- Desktop Menu -->
            <ul class="hidden md:flex gap-2 list-none bg-white/5 p-1.5 rounded-xl border border-white/5 backdrop-blur-sm">
                <li v-for="link in navLinks" :key="link.name">
                    <a @click.prevent="scrollToSection(link.href)" 
                       :class="['px-6 py-2 rounded-lg cursor-pointer transition-all duration-300 font-medium text-sm relative overflow-hidden group', 
                                activeSection === link.href ? 'text-white' : 'text-text-secondary hover:text-white']">
                        <span class="relative z-10">{{ link.name }}</span>
                        <!-- Active Indicator -->
                        <div v-if="activeSection === link.href" 
                             class="absolute inset-0 bg-accent-blue/20 border-b-2 border-accent-blue z-0 transition-all duration-500"></div>
                        <!-- Hover Effect -->
                        <div class="absolute inset-0 bg-white/5 scale-x-0 group-hover:scale-x-100 transition-transform duration-300 origin-left"></div>
                    </a>
                </li>
            </ul>

            <!-- Mobile Menu Toggle -->
            <div class="md:hidden relative w-10 h-10 flex flex-col justify-center items-center cursor-pointer z-[60] bg-white/5 rounded-full border border-white/10" @click="toggleMenu">
                <span :class="['w-5 h-[1.5px] bg-white transition-all duration-300 rounded-full', isMenuOpen ? 'rotate-45 translate-y-[1px]' : '-translate-y-1.5']"></span>
                <span :class="['w-5 h-[1.5px] bg-white transition-all duration-300 rounded-full', isMenuOpen ? 'opacity-0' : 'opacity-100']"></span>
                <span :class="['w-5 h-[1.5px] bg-white transition-all duration-300 rounded-full', isMenuOpen ? '-rotate-45 -translate-y-[1px]' : 'translate-y-1.5']"></span>
            </div>

            <!-- Mobile Menu -->
            <transition name="menu-fade">
                <div v-if="isMenuOpen" 
                     class="fixed inset-0 h-screen w-full bg-[#0a0e27]/95 backdrop-blur-2xl z-50 flex flex-col justify-center items-center overflow-hidden">
                    
                    <!-- Decor Elements -->
                    <div class="absolute top-[-10%] left-[-10%] w-[40%] h-[40%] bg-accent-blue/10 blur-[120px] rounded-full"></div>
                    <div class="absolute bottom-[-10%] right-[-10%] w-[50%] h-[50%] bg-accent-blue/5 blur-[150px] rounded-full"></div>

                    <div class="flex flex-col gap-8 items-center relative z-[51]">
                        <a v-for="(link, index) in navLinks" 
                           :key="link.name"
                           @click.prevent="scrollToSection(link.href)"
                           :style="{ transitionDelay: `${index * 100}ms` }"
                           :class="['text-4xl font-bold transition-all duration-500 hover:tracking-widest relative group', 
                                    activeSection === link.href ? 'text-accent-blue' : 'text-white/60 hover:text-white',
                                    isMenuOpen ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0']">
                            <span class="text-sm font-mono text-accent-blue/40 mr-4">0{{ index + 1 }}</span>
                            {{ link.name }}
                        </a>
                    </div>

                    <!-- Socials / Info in Mobile Menu -->
                    <div class="mt-24 text-text-secondary text-sm flex gap-8 relative z-[51]">
                        <span class="hover:text-accent-blue cursor-pointer transition-colors">LinkedIn</span>
                        <span class="hover:text-accent-blue cursor-pointer transition-colors">GitHub</span>
                        <span class="hover:text-accent-blue cursor-pointer transition-colors">Instagram</span>
                    </div>
                </div>
            </transition>
        </nav>
    </header>
</template>

<style scoped>
.menu-fade-enter-active,
.menu-fade-leave-active {
    transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.menu-fade-enter-from,
.menu-fade-leave-to {
    opacity: 0;
    backdrop-filter: blur(0px);
}

/* Hide scrollbar for the mobile menu links container if needed */
.hide-scrollbar::-webkit-scrollbar {
    display: none;
}
.hide-scrollbar {
    -ms-overflow-style: none;
    scrollbar-width: none;
}
</style>

