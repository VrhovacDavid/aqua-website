<!-- Home.vue -->
<template>
    <div class="relative w-full h-screen bg-cover bg-center"
        style="background-image: url('/src/assets/background.jpg');">

        <div class="absolute inset-0 flex gap-x-8 m-2">
            <p class="text-xl font-medium text-center text-black mb-80">
                Wer sind wir?
            </p>
            <p class="text-xl font-medium text-center text-black mb-80">
                Lust, Teil des Teams zu werden?
            </p>
        </div>
        <!-- Centered text -->
        <div class="absolute inset-0 flex justify-center items-center">
            <h1 class="text-2xl font-bold text-center text-black mb-80 font-custom">
                Deine umweltfreundliche Reinigungsfirma aus der Ostschweiz. <br />
                Seit über 20 Jahren.
            </h1>
        </div>

        <div class="absolute inset-0 flex">
            <!-- Main content area -->
            <div class="flex-grow flex flex-col justify-end">
                <!-- Bottom containers -->
                <div class="flex h-64">
                    <div v-for="(item, index) in services" :key="index" @click="openPopup(item.name)"
                        class="relative flex-1 p-4 m-2 aspect-square flex items-center justify-center rounded-xl shadow-xl cursor-pointer overflow-hidden">
                        <div class="absolute inset-0 bg-white opacity-35"></div>
                        <p class="font-bold relative z-10">{{ item.name }}</p>
                    </div>
                </div>
            </div>
     
            <!-- Long container on the right -->

            
            <div class="relative w-1/6 p-4 flex flex-col rounded-xl shadow-xl overflow-hidden">
                <div class="absolute inset-0 bg-white opacity-35"></div>
                <div class="relative z-10 flex flex-col h-full">
                    <div class="text-center mb-4">
                        <p class="text-center font-bold text-xl font-custom">Unsere geschätzten Kundinnen und Kunden</p>
                    </div>
                    <div class="flex-grow flex flex-col justify-center items-center space-y-16">
                        <img src="/src/assets/stgallen.png" alt="St. Gallen" class="w-48 h-16 object-contain">
                        <img src="/src/assets/bauer.png" alt="Bauer" class="w-48 h-16 object-contain">
                        <img src="/src/assets/manor.png" alt="Manor" class="w-48 h-16 object-contain">
                        <img src="/src/assets/hev.png" alt="HEV" class="w-48 h-16 object-contain">
                    </div>
                </div>
            </div>
        </div>

        <PopupForm :isOpen="isPopupOpen" @close="closePopup" :initialService="selectedService" :services="services" />
    </div>
</template>

<script>
import PopupForm from '/src/components/PopupForm.vue';

export default {
    name: 'Home',
    components: {
        PopupForm
    },
    data() {
        return {
            isPopupOpen: false,
            selectedService: '',
            services: [
                { name: 'Umzugsreinigung', image: 'https://img.freepik.com/free-photo/happy-couple-moving-their-new-home_23-2149749195.jpg?t=st=1723153240~exp=1723156840~hmac=afece08024c381354aece2cc0977beb66f0c6d4e515b68abf063f6067a19a36f&w=996' },
                { name: 'Büroreinigung', image: 'https://img.freepik.com/free-photo/front-view-off-office-desk_23-2149034544.jpg?t=st=1723153247~exp=1723156847~hmac=553f49405cd98a238d70abae84775a3c60915e2314265afd9f30d88607b29166&w=740' },
                { name: 'Hauswartung', image: 'https://img.freepik.com/free-photo/service-maintenance-worker-repairing_23-2149176722.jpg?t=st=1723153293~exp=1723156893~hmac=31001e3ff78f2e160182095b3a7f877e1589ad8fccc660a8577dd4bcf7e056ed&w=996' },
                { name: 'Baureinigung', image: 'https://img.freepik.com/free-photo/residential-house-process-building_23-2147694705.jpg?t=st=1723153315~exp=1723156915~hmac=be3d281466baefd2939e4d10eacbb69d17f6dcc3f13914132885ee303f1d3568&w=996' },
            ]
        }
    },
    methods: {
        openPopup(service) {
            this.selectedService = service;
            this.isPopupOpen = true;
        },
        closePopup() {
            this.isPopupOpen = false;
        }
    }
}
</script>