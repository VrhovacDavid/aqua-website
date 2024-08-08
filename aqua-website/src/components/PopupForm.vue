<!-- PopupForm.vue -->
<template>
  <div v-if="isOpen" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-lg p-6 w-full max-w-4xl flex">
      <!-- Form Column -->
      <div class="w-1/2 pr-4">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-bold">Dienstleistungsanfrage</h2>
          <button @click="$emit('close')" class="text-gray-500 hover:text-gray-700">
            <span class="text-2xl">&times;</span>
          </button>
        </div>
        <form @submit.prevent="submitForm">
          <div class="mb-4 flex gap-4">
            <div class="flex-1">
              <label for="vorname" class="block mb-2">Vorname</label>
              <input type="text" id="vorname" v-model="formData.vorname" class="w-full p-2 border rounded" required />
            </div>
            <div class="flex-1">
              <label for="nachname" class="block mb-2">Nachname</label>
              <input type="text" id="nachname" v-model="formData.nachname" class="w-full p-2 border rounded" required />
            </div>
          </div>
          <div class="mb-4">
            <label for="adresse" class="block mb-2">Adresse</label>
            <input type="text" id="adresse" v-model="formData.adresse" class="w-full p-2 border rounded" required />
          </div>
          <div class="mb-4">
            <label for="plzOrt" class="block mb-2">PLZ/Ort</label>
            <input type="text" id="plzOrt" v-model="formData.plzOrt" class="w-full p-2 border rounded" required />
          </div>
          <div class="mb-4">
            <label class="block mb-2">Services</label>
            <div v-for="service in services" :key="service.name" class="flex items-center mb-2">
              <input type="checkbox" :id="service.name" v-model="formData.selectedServices" :value="service.name"
                class="mr-2">
              <label :for="service.name">{{ service.name }}</label>
            </div>
          </div>
          <div class="mb-4">
            <label for="nachricht" class="block mb-2">Nachricht</label>
            <textarea id="nachricht" v-model="formData.nachricht" class="w-full p-2 border rounded" rows="4"
              required></textarea>
          </div>
          <button type="submit" class="w-full bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600">
            Absenden
          </button>
        </form>
      </div>

      <!-- Image Column -->
      <div class="w-1/2 pl-4 flex items-center justify-center">
        <img :src="currentImage" :alt="currentService" class="max-w-full h-full object-cover rounded-lg shadow-lg" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PopupForm',
  props: {
    isOpen: Boolean,
    initialService: String,
    services: Array,
  },
  data() {
    return {
      formData: {
        vorname: '',
        nachname: '',
        adresse: '',
        plzOrt: '',
        selectedServices: [],
        nachricht: '',
      },
      currentService: '',
    };
  },
  computed: {
    currentImage() {
      const service = this.services.find(s => s.name === this.currentService);
      return service ? service.image : '';
    }
  },
  watch: {
    initialService(newService) {
      this.currentService = newService;
      if (!this.formData.selectedServices.includes(newService)) {
        this.formData.selectedServices.push(newService);
      }
    },
    'formData.selectedServices': {
      handler(newServices) {
        if (newServices.length > 0 && !this.currentService) {
          this.currentService = newServices[0];
        } else if (newServices.length === 0) {
          this.currentService = '';
        }
      },
      deep: true
    }
  },
  methods: {
    submitForm() {
      console.log('Form submitted:', this.formData);
      this.$emit('close');
    },
  },
};
</script>