<template>
  <div class="min-h-screen bg-gray-100">
    <div class="container py-6">
      <div class="bg-white p-4 rounded">
        <div class="flex -mx-4 items-center mb-6">
          <div class="flex-1 px-4">
            <select class="quran-input" name="" id="">
              <option value="">Select Sura</option>
              <option v-for="sura in suras" value="">
                {{ sura.name }} - {{ sura.englishName }}
              </option>
            </select>
          </div>

          <div class="flex-1 px-4 text-center">
            <h3 class="font-bold mb-1 text-lg">Al-Baqarah</h3>
            <p>The Cow</p>
          </div>

          <div class="flex-1 px-4">
            <select class="quran-input" name="" id="">
              <option value="">Select Ayah</option>
            </select>
          </div>
        </div>

        <div class="text-4xl">
          <p
            class="flex items-center mb-6"
            v-if="currentSura.hasOwnProperty('ayahs')"
            v-for="ayah in currentSura.ayahs"
          >
            <span
              class="text-sm mr-4 flex items-center justify-center inline-block w-5 h-5 border rounded-full"
              >{{ ayah.number }}</span
            >
            {{ ayah.text }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      suras: [],
      currentSura: [],
    };
  },
  mounted() {
    axios.get("https://api.alquran.cloud/v1/surah").then((res) => {
      this.suras = res.data.data;
    });
    axios.get("https://api.alquran.cloud/v1/surah/1").then((res) => {
      console.log(res.data.data);
      this.currentSura = res.data.data;
    });
  },
};
</script>
