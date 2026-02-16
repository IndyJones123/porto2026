<script setup lang="ts">
import { ref, computed } from 'vue';
import Dialog from 'primevue/dialog';

interface ProjectImage {
    url: string;
    description: string;
}

interface TabContent {
    mainText: string;
    items: ProjectImage[];
}

interface ProjectDetails {
    overview: TabContent;
    features: TabContent;
    responsibilities: TabContent;
}

interface Project {
    id: string;
    title: string;
    desc: string;
    tags: string[];
    icon: string;
    gradient: string;
    link?: string;
    details?: ProjectDetails;
}

const visible = ref(false);
const activeTab = ref(0);
const activeImageIndex = ref(0);
const selectedProject = ref<Project | null>(null);

const projects: Project[] = [
    {
        id: 'marketplace',
        title: 'OG x AOR Marketplace',
        desc: 'High-performance cross-server trading platform for OG x AOR.',
        tags: ['FastAPI', 'React', 'PostgreSQL'],
        icon: '🎮',
        gradient: 'from-[#4a9eff] to-[#7db9ff]',
        link: 'https://rog-market.com/',
        details: {
            overview: {
                mainText: 'A specialized marketplace system designed to facilitate item trading across multiple game servers.',
                items: [
                    { url: 'markethero.png', description: 'Centralized Marketplace RMT ( Real Money Trading ) System for OG x AOR Official Server.' },
                ]
            },
            features: {
                mainText: 'Advanced transactional features ensuring speed and security.',
                items: [
                    { url: 'topup.png', description: 'Topup System Integration Using QR CODE QRIS, VA BANK from duitku payment gateway for OG x AOR Official Server.' },
                     { url: '/market.png', description: 'Marketplace System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.' },
                     { url: '/marketauction.png', description: 'Livetime Auction System + Livechat System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.' },
                     { url: '/marketflashsale.jpg', description: 'Flash Sale System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.' },
                     { url: '/markethistory.png', description:'History Action System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.'},
                     { url: '/marketchart.png', description:'Livetime Market Chart Price System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.'},
                     { url: '/marketragpoly.png', description:'Ragpoly Monopoloy Game Gacha System Integration for OG x AOR Official Server.'},
                     { url: '/marketwithdrawal.png', description:'Withdrawal System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.'},
                     { url: '/marketnpc.gif', description:'NPC System Integration Selling Item RMT ( Real Money Trading ) for OG x AOR Official Server.'},
                     { url: '/markethook.jpg', description:'Market Hook For Withdrawal , Bidding , Auction , Flash Sale , Transaction System Integration Using Discord Hook BOT Server for OG x AOR Official Server.'},
                     { url: '/marketofficial.png', description:'And Many More Features Details can be checked on the official wikipedia server. https://aorxog.gitbook.io/wiki/server-feature/marketplace-hot'}
                ]
            },
responsibilities: {
    mainText: 'Lead Developer responsible for end-to-end implementation.',
    items: [
        { 
            url: '/absolutecinema.png', 
            description: 'Handled full end-to-end development lifecycle: gathering and analyzing business requirements, system architecture design, and translating them into scalable technical solutions. Implemented both frontend and backend systems, designed high-performance PostgreSQL schemas, and built secure REST APIs. Managed deployment and infrastructure configuration via Cloudflare, including DNS, caching, WAF, and performance optimization. Implemented structured logging, monitoring, and error tracking for production stability. Conducted security hardening and penetration testing to ensure system resilience, data protection, and compliance with best security practices.'
        }
    ]
}

        }
    },
    {
        id: 'apbisdi',
        title: 'APBISDI.id Website',
        desc: 'Platform for Digital Business Professionals and Educators in Indonesia.',
        tags: ['Laravel', 'PHP', 'SEO'],
        icon: '🎓',
        gradient: 'from-[#6366f1] to-[#a855f7]',
        link: 'https://apbisdi.id',
        details: {
            overview: {
                mainText: 'The official digital hub for the Association of Digital Business Professionals and Educators.',
                items: [
                    { url: '/apbisdi1.png', description: 'Clean, professional landing page designed for easy navigation of academic standards.' }
                ]
            },
            features: {
                mainText: 'Tools for professional growth and academic collaboration.',
                items: [
                    { url: '/apbisdi2.png', description: 'Membership management portal with institution-level controls and reporting.' },
                    { url: '/apbisdi3.png', description: 'Membership management portal with institution-level controls and reporting.' },
                    { url: '/apbisdi4.png', description: 'Dashboard for easy navigation of academic standards.' },
                    { url: '/apbisdi5.png', description: 'Dynamic SMTP email notifications for membership updates.' },
                    
                ]
            },
            responsibilities: {
                mainText: 'Full-stack development and SEO optimization.',
                items: [
                    { url: '/apbisdi6.png', description: 'Fully built website with all features. With Preparing Presentation and Annual Meeting Report 2024.' },
                ]
            }
        }
    },
    {
        id: 'banking',
        title: 'Mitrasoft Core Banking',
        desc: 'Enterprise-grade modules for Sharia banking operations. [Confidential - NDA]',
        tags: ['Python', 'FastAPI', 'Vue.js', 'Flutter', 'Syariah Banking'],
        icon: '🏦',
        gradient: 'from-[#10b981] to-[#34d399]',
        details: {
            overview: {
                mainText: 'Development of surrounding internal and client-facing applications for Sharia banking.',
                items: [
                    { url: 'https://media.licdn.com/dms/image/C560BAQHUtxl3EQW7xQ/company-logo_200_200/0/1631176976860/pt_mitraosft_global_perdana_logo?e=2147483647&v=beta&t=OB672bQxtwbTkoGo5eP6Gg_F7xKAqBhfR9SfGumTyqo', description: 'Integrated within the Mitrasoft Global Perdana ecosystem.' }
                ]
            },
            features: {
                mainText: 'Secure and compliant financial operation modules.',
                items: [
                    { url: '/confidential.png', description: 'Confidential feature implementation.' }
                ]
            },
            responsibilities: {
                mainText: 'Backend development focus for surrounding applications.',
                items: [
                    { url: '/confidential.png', description: 'Developed custom clients and internal service.' }
                ]
            }
        }
    },
    
];

const openModal = (project: Project) => {
    if (project.details) {
        selectedProject.value = project;
        activeTab.value = 0;
        activeImageIndex.value = 0;
        visible.value = true;
    }
};

const tabs = ['Overview', 'Features', 'Responsibilities'];

const getCurrentTabDetails = computed(() => {
    const p = selectedProject.value;
    if (!p || !p.details) return null;
    const tabName = tabs[activeTab.value];
    if (!tabName) return null;
    const key = tabName.toLowerCase();
    return (p.details as any)[key] as TabContent;
});

const currentImage = computed(() => {
    const details = getCurrentTabDetails.value;
    if (!details || !details.items || details.items.length === 0) return '';
    const imgItem = details.items[activeImageIndex.value];
    return resolvePath(imgItem?.url || details.items[0]?.url || '');
});

const resolvePath = (url: string | undefined) => {
    if (!url) return '';
    // Keep external URLs and data URIs as-is
    if (/^(https?:)?\/\//.test(url) || url.startsWith('data:')) return url;
    
    const base = import.meta.env.BASE_URL || '/';
    // Ensure base ends with / and url doesn't start with /
    const cleanBase = base.endsWith('/') ? base : `${base}/`;
    const cleanUrl = url.startsWith('/') ? url.slice(1) : url;
    
    return `${cleanBase}${cleanUrl}`;
};

const currentContent = computed(() => {
    const details = getCurrentTabDetails.value;
    if (!details) return '';
    const imgItem = details.items[activeImageIndex.value];
    // Show image description if available, otherwise fallback to mainText
    return imgItem?.description || details.mainText || '';
});

const getProjectAccent = computed(() => {
    if (!selectedProject.value) return '#4a9eff';
    const gradient = selectedProject.value.gradient;
    const match = gradient.match(/\[(#[0-9a-fA-F]{3,6})\]/);
    return match ? match[1] : '#4a9eff';
});






</script>

<template>
    <section class="py-24 px-[5%] bg-bg-primary" id="projects">
        <div class="max-w-[1200px] mx-auto">
            <div class="mb-16">
                 <span class="text-accent-blue font-semibold uppercase tracking-widest text-sm mb-4 block">Portfolio</span>
                <h2 class="text-4xl font-bold mb-4">Featured Projects</h2>
                <p class="text-text-secondary text-lg max-w-2xl">Showcasing real-world enterprise solutions and specialized platform developments.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div v-for="project in projects" :key="project.id" 
                     class="bg-bg-card rounded-xl overflow-hidden border border-accent-blue/10 hover:-translate-y-2 hover:border-accent-blue hover:shadow-[0_10px_30px_rgba(74,158,255,0.2)] transition-all duration-300 group cursor-pointer"
                     @click="openModal(project)">
                    
                    <!-- Improved Project Thumbnail -->
                    <div class="relative h-[220px] overflow-hidden">
                            <img v-if="project.details?.overview.items[0]" 
                                :src="resolvePath(project.details.overview.items[0].url)" 
                                class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110" 
                                alt="Thumbnail">
                        <div v-else :class="['w-full h-full flex items-center justify-center text-5xl bg-gradient-to-br', project.gradient]">
                            {{ project.icon }}
                        </div>
                        <!-- Overlay for Icon -->
                        <div class="absolute top-4 right-4 w-12 h-12 rounded-lg bg-bg-card/80 backdrop-blur-sm border border-white/10 flex items-center justify-center text-2xl">
                            {{ project.icon }}
                        </div>
                    </div>

                    <div class="p-8">
                        <h3 class="text-2xl text-whitefont-semibold mb-4">{{ project.title }}</h3>
                        <p class="text-text-secondary mb-6 leading-relaxed line-clamp-2 h-[3rem]">{{ project.desc }}</p>
                        <div class="flex gap-2 flex-wrap mb-6">
                            <span v-for="tag in project.tags" :key="tag" class="px-3 py-1 bg-accent-blue/10 rounded-full text-sm text-accent-blue">
                                {{ tag }}
                            </span>
                        </div>
                        <div class="flex justify-between items-center">
                            <button class="text-accent-blue font-semibold inline-flex items-center gap-2 group-hover:gap-4 transition-all">
                                View Details <span>→</span>
                            </button>
                            <a v-if="project.link" :href="project.link" @click.stop target="_blank" class="text-text-secondary hover:text-white transition-colors">
                                <i class="pi pi-external-link">Live Website</i>
                            </a>
                            <p v-else>Confidential</p>
                        </div>
                    </div>
                </div>
            </div>

            <Dialog v-model:visible="visible" 
                    modal 
                    :header="selectedProject?.title" 
                    :style="{ width: '95vw', maxWidth: '1100px', backgroundColor: '#0a0e27' }" 
                    class="bg-[#0a0e27]"
                    :pt="{ 
                        root: { class: 'bg-[#0a0e27] border border-white/10 rounded-3xl text-white shadow-[0_0_50px_rgba(0,0,0,0.5)] overflow-hidden' }, 
                        
                        content: { class: 'bg-transparent p-0' }, 
                        closeButton: { class: 'text-white hover:bg-white/10 transition-all rounded-full p-2' },
                        mask: { class: 'backdrop-blur-sm bg-black/60' }
                    }">
                <div class="flex flex-col md:flex-row  h-[85vh] md:h-[750px] overflow-hidden relative bg-[#0a0e27]">
                    <!-- Dynamic Glow Background -->
                    <div class="absolute inset-0 pointer-events-none opacity-20"
                         :style="{ background: `radial-gradient(circle at 50% 50%, ${getProjectAccent} 0%, transparent 70%)` }"></div>


                    <!-- Sidebar Menu -->
                    <div class="w-full md:w-[260px] bg-white/5 border-b md:border-b-0 md:border-r border-white/10 flex md:flex-col overflow-x-auto md:overflow-visible flex-shrink-0 relative z-10">


                        <button v-for="(tab, index) in tabs" :key="tab" 
                                @click="activeTab = index; activeImageIndex = 0"
                                :class="['px-8 py-6 text-left transition-all relative group', activeTab === index ? 'text-white' : 'text-gray-400 hover:text-white']">
                            <span class="relative z-10 flex items-center gap-4">
                                <span :class="['w-1.5 h-1.5 rounded-full transition-all duration-500', activeTab === index ? 'scale-100 opacity-100' : 'scale-0 opacity-0']"
                                      :style="{ backgroundColor: getProjectAccent, boxShadow: `0 0 15px ${getProjectAccent}` }"></span>
                                <span class="font-medium tracking-wide uppercase text-xs">{{ tab }}</span>
                            </span>
                            <div v-if="activeTab === index" 
                                 class="absolute inset-0 bg-white/5 border-r-[3px] z-0 transition-all duration-500"
                                 :style="{ borderRightColor: getProjectAccent }"></div>
                        </button>


                    </div>


                    <!-- Content Area -->
                    <div class="flex-1 p-6 md:p-10 overflow-y-auto bg-gradient-to-br from-transparent to-white/5 relative z-10">
                        <div v-if="selectedProject?.details && getCurrentTabDetails" class="space-y-10 animate-in fade-in slide-in-from-bottom-4 duration-500">
                            <!-- Image Gallery Container -->
                            <div class="space-y-6">
                                <div class="relative group aspect-video overflow-hidden rounded-2xl border border-white/10 shadow-2xl bg-black/40">
                                    <transition name="fade" mode="out-in">
                                        <img :key="currentImage" :src="currentImage" class="w-full h-full object-contain" alt="Preview">
                                    </transition>
                                    
                                    <!-- Image Navigation Arrows -->
                                    <div v-if="getCurrentTabDetails.items && getCurrentTabDetails.items.length > 1" class="absolute inset-0 flex items-center justify-between px-4 opacity-0 group-hover:opacity-100 transition-opacity">
                                        <button @click="activeImageIndex = (activeImageIndex > 0 ? activeImageIndex - 1 : getCurrentTabDetails.items.length - 1)"
                                                class="w-12 h-12 rounded-full bg-black/60 backdrop-blur-md flex items-center justify-center border border-white/10 hover:bg-black/80 transition-all transform hover:scale-110">
                                            <i class="pi pi-chevron-left text-xl"></i>
                                        </button>
                                        <button @click="activeImageIndex = (activeImageIndex < getCurrentTabDetails.items.length - 1 ? activeImageIndex + 1 : 0)"
                                                class="w-12 h-12 rounded-full bg-black/60 backdrop-blur-md flex items-center justify-center border border-white/10 hover:bg-black/80 transition-all transform hover:scale-110">
                                            <i class="pi pi-chevron-right text-xl"></i>
                                        </button>
                                    </div>

                                    <!-- Counter Overlay -->
                                    <div v-if="getCurrentTabDetails.items && getCurrentTabDetails.items.length > 1" 
                                         class="absolute bottom-4 right-4 px-3 py-1 rounded-full bg-black/60 backdrop-blur-md border border-white/10 text-xs font-medium text-white/80">
                                        {{ activeImageIndex + 1 }} / {{ getCurrentTabDetails.items.length }}
                                    </div>
                                </div>

                                <!-- Thumbnails Navigation -->
                                <div v-if="getCurrentTabDetails.items && getCurrentTabDetails.items.length > 1" class="flex gap-4 overflow-x-auto pb-2 custom-scrollbar">
                                    <div v-for="(img, idx) in getCurrentTabDetails.items" :key="idx"
                                         @click="activeImageIndex = idx"
                                         :class="['w-24 h-16 rounded-xl overflow-hidden border-2 cursor-pointer transition-all flex-shrink-0 relative group', activeImageIndex === idx ? 'scale-105 z-10' : 'opacity-40 hover:opacity-100']"
                                         :style="{ borderColor: activeImageIndex === idx ? getProjectAccent : 'rgba(255,255,255,0.1)' }">
                                        <img :src="resolvePath(img.url)" class="w-full h-full object-cover" alt="Thumb">
                                        <div v-if="activeImageIndex === idx" class="absolute inset-0 bg-white/10"></div>
                                    </div>
                                </div>
                            </div>

                            <!-- Text Content -->
                            <div class="space-y-6">
                                <div class="flex items-center gap-4">
                                    <div class="h-10 w-1 flex-shrink-0 rounded-full" :style="{ backgroundColor: getProjectAccent }"></div>
                                    <h4 class="text-3xl text-white font-bold tracking-tight">{{ tabs[activeTab] }}</h4>
                                </div>
                                <div class="bg-white/5 rounded-2xl p-8 border border-white/10 relative overflow-hidden group">
                                     <!-- Decorative Corner -->
                                    <div class="absolute -top-4 -right-4 w-12 h-12 transition-all duration-500 group-hover:scale-150 rotate-45"
                                         :style="{ backgroundColor: `${getProjectAccent}20` }"></div>
                                    
                                    <p class="text-gray-300 text-lg leading-relaxed whitespace-pre-line relative z-10">
                                        {{ currentContent }}
                                    </p>
                                </div>


                            </div>
                        </div>
                    </div>
                </div>
            </Dialog>

        </div>
    </section>
</template>

<style scoped>
.line-clamp-2 {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

/* Custom Scrollbar for the modal content */
.custom-scrollbar::-webkit-scrollbar {
    height: 4px;
    width: 4px;
}
.custom-scrollbar::-webkit-scrollbar-track {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 10px;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.2);
    border-radius: 10px;
}
.custom-scrollbar::-webkit-scrollbar-thumb:hover {
    background: rgba(255, 255, 255, 0.3);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

::-webkit-scrollbar {
    width: 6px;
    height: 6px;
}
::-webkit-scrollbar-track {
    background: transparent; 
}
::-webkit-scrollbar-thumb {
    background: rgba(74, 158, 255, 0.3); 
    border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
    background: rgba(74, 158, 255, 0.5); 
}
</style>
