<template>
  <button @click="openModal"
    class="text-gray-900 dark:text-white dark:hover:text-gray-400 hover:text-gray-800 hover:bg-gray-200 dark:hover:bg-gray-700 hover:rounded-lg py-2 px-2 text-xl focus:outline-none leading-none rounded">
    <font-awesome-icon :icon="['far', 'eye']" />
  </button>
  <DialogModal :show="isModalOpen" :closeable="true" @close="handleCloseModal">
    <template #content>
      <div>
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
          <div class="flex justify-center">
            <button @click="page = page > 1 ? page - 1 : page" class="text-gray-800 p-4 text-xl">
              <font-awesome-icon :icon="['fas', 'caret-left']" />
            </button>
            <span class="mt-5">{{ page }} / {{ pages }}</span>
            <button @click="page = page < pages ? page + 1 : page" class="text-gray-800 p-4 text-xl">
              <font-awesome-icon :icon="['fas', 'caret-right']" />
            </button>
          </div>
          <div class="border-t-2 flex justify-center">
            <h1 v-if="page <= 0" class="dark:text-white text-center text-9xl">File pdf tidak ditemukan</h1>
            <VuePDF :pdf="pdf" :page="page" :scale="1.25" />
          </div>
        </div>
      </div>
    </template>
    <template #footer>
      <button @click="handleCloseModal" class="bg-gray-800 hover:bg-gray-900 text-white px-4 py-2 rounded">
        Tutup
      </button>
    </template>
  </DialogModal>
</template>

<script>
import DialogModal from './DialogModal.vue';
import { VuePDF, usePDF } from '@tato30/vue-pdf';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import axios from 'axios';

export default {
  components: {
    DialogModal,
    FontAwesomeIcon,
    VuePDF
  },
  props: {
    surat_file: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isModalOpen: false,
      pdf: null,
      pages: null,
      page: 1,
      pdfPath: null
    };
  },
  mounted() {
    console.log(this.surat_file);
    axios.get(`https://astek.up.railway.app/api/get-pdf/${this.surat_file}`, {
      responseType: "blob"
    })
      .then(response => {
        console.log("Success", response);
        const blob = new Blob([response.data], { type: 'application/pdf' });
        const objectUrl = URL.createObjectURL(blob);
        this.pdfPath = objectUrl;
        this.initializePDF();
      })
      .catch(error => {
        console.error("Error fetching PDF:", error);
      });
  },
  methods: {
    handleCloseModal() {
      if (this.pdfPath) {
        URL.revokeObjectURL(this.pdfPath);
        this.pdfPath = null;
      }
      location.reload();
      this.isModalOpen = false;
    },
    openModal() {
      this.reinitializePDF();
      this.isModalOpen = true;
    },
    initializePDF() {
      const { pdf, pages } = usePDF(this.pdfPath);
      this.pdf = pdf;
      this.pages = pages;
    },
    reinitializePDF() {
      this.initializePDF();
    },
  },
};
</script>
