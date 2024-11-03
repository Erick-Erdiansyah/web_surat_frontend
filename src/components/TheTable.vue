<script>
import WelcomeItem from './WelcomeItem.vue';
import DocumentationIcon from './icons/IconDocumentation.vue';
import axios from 'axios';
import ReadModal from './ReadModal.vue';

export default {
  components: {
    WelcomeItem,
    DocumentationIcon,
    ReadModal,
  },
  data() {
    return {
      laporans: null,
    };
  },
  mounted() {
    axios
      .get("https://astek.up.railway.app/api/")
      .then(response => {
        this.laporans = response.data.laporans;
        console.log(this.laporans);
      })
      .catch(error => {
        console.error("Error fetching data:", error);
      });
  },
  methods: {
    FileName(value) {
      let fileName = value.toString().replace('surat_files/', '');
      return fileName;
    }
  }
};
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>List Surat</template>
    <div class="sm:pb-6 lg:py-3 max-w-7xl mx-auto sm:px-6 lg:px-6  bg-gray-600  rounded-lg opacity-80">
      <div class="mb-2">
        <input type="text" class="border rounded-lg" placeholder="Cari...">
      </div>
      <div class="bg-gray-200 opacity-100 overflow-hidden max-h-[1000px] overflow-y-auto shadow-xl sm:rounded-lg">
        <table class="mx-auto lg:mx-0 min-w-full divide-y divide-gray-200">
          <tbody class="bg-white divide-y divide-gray-200">
            <template v-if="laporans && laporans.length">
              <tr v-for="item in laporans" :key="item.id"
                class="hover:bg-slate-100 dark:hover:bg-slate-800 dark:bg-slate-700 relative">
                <td class="px-4 py-2 whitespace-pre-wrap lg:w-60">
                  <div class="flex items-center">
                    <p
                      class="text-sm px-3 pt-1 rounded-sm text-white dark:text-black dark:bg-white bg-slate-900 lg:w-40 sm:w-32 flex items-center absolute top-0 left-0">
                      {{ item.created_human }}
                    </p>
                    <div class="flex items-center">
                      <p class="text-gray-900 dark:text-white text-base pt-2 font-medium">{{ item.judul }}</p>
                    </div>
                  </div>
                </td>
                <td class="w-36"></td>
                <td>
                  <div class="flex items-center mx-3">
                    <ReadModal :surat_file="FileName(item.surat_file)" />
                  </div>
                </td>
              </tr>
            </template>
            <tr v-else>
              <td colspan="5" class="text-center">No data available.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </WelcomeItem>
</template>
