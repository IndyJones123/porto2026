<script setup lang="ts">
const scrollToSection = (id: string) => {
    const element = document.getElementById(id);
    if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
    }
};
</script>

<template>
    <section class="min-h-screen flex items-center px-[5%] mt-20" id="home">
        <div class="max-w-[1200px] mx-auto w-full grid grid-cols-1 lg:grid-cols-[1.2fr_0.8fr] gap-16 items-center">
            <div class="order-2 lg:order-1 text-center lg:text-left">
                <span class="text-accent-blue font-semibold uppercase tracking-widest text-sm mb-4 block">✨ Software Developer</span>
                <h1 class="text-4xl md:text-6xl lg:text-7xl font-bold mb-6 leading-[1.1]">
                    Hi, I'm <span class="text-accent-blue">AlfianDev</span><br>Software Engineer
                </h1>
                <p class="text-lg md:text-xl text-text-secondary mb-10 leading-relaxed max-w-2xl mx-auto lg:mx-0">
                    I build clean, modern web applications with a focus on user experience and performance. Let's create something amazing together!
                </p>
                <div class="flex gap-4 flex-wrap justify-center lg:justify-start">
                    <button @click="scrollToSection('projects')" class="px-8 py-4 bg-accent-blue text-bg-primary font-semibold rounded-lg hover:bg-accent-light hover:-translate-y-0.5 transition-all duration-300">
                        View Projects
                    </button>
                    <button @click="scrollToSection('contact')" class="px-8 py-4 bg-transparent text-accent-blue border-2 border-accent-blue font-semibold rounded-lg hover:bg-accent-blue/10 transition-all duration-300">
                        Contact Me
                    </button>
                </div>
            </div>

            <div class="order-1 lg:order-2 relative flex justify-center items-center [perspective:1000px] group">
                <!-- Outer Container with 3D Flip -->
                <div class="relative w-full max-w-[400px] h-[600px] transition-all duration-700 [transform-style:preserve-3d] group-hover:[transform:rotateY(180deg)] cursor-pointer">
                    
                    <!-- Front Image (Alfian AI) -->
                    <div class="absolute inset-0 w-full h-full [backface-visibility:hidden]">
                        <img src="/alfianai.jpg" alt="Alfian - Software Developer" 
                             class="w-full h-full object-cover rounded-3xl border-2 border-accent-blue shadow-[0_0_30px_rgba(74,158,255,0.3)]">
                        <!-- Dreamy Glow Overlay -->
                        <div class="absolute inset-0 rounded-3xl bg-gradient-to-t from-accent-blue/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
                    </div>

                    <!-- Back Image (Istri Alfian) -->
                    <div class="absolute inset-0 w-full h-full [backface-visibility:hidden] [transform:rotateY(180deg)]">
                        <img src="/istrialfian.png" alt="Special Version" 
                             class="w-full h-full object-cover rounded-3xl border-2 border-accent-rabbit shadow-[0_0_40px_rgba(255,179,217,0.4)]">
                        <!-- "Halu" Sparks/Glow -->
                        <div class="absolute inset-0 rounded-3xl bg-gradient-to-tr from-accent-rabbit/30 via-transparent to-accent-blue/30"></div>
                        <div class="absolute -inset-4 bg-accent-rabbit/10 blur-2xl rounded-full -z-10 animate-pulse"></div>
                    </div>
                </div>

                <!-- Global Glow effect -->
                <div class="absolute w-[120%] h-[120%] bg-accent-blue blur-[120px] opacity-10 z-0 pointer-events-none group-hover:bg-accent-rabbit transition-colors duration-700"></div>
            </div>

        </div>
    </section>
</template>
