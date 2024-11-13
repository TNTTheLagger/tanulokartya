<template>
  <div class="container">
    <h1 class="text-center">Tanulókártya Alkalmazás</h1>
    <KartyaForm
      :kartya-to-edit="currentEditKartya"
      @add-kartya="addKartya"
      @update-kartya="updateKartya"
      @clear-edit="clearEdit"
    />
    <div class="mt-4">
      <h5>Kész kártyák</h5>
      <div class="mb-3">
        <select v-model="filterDifficulty" class="form-select" aria-label="Szűrés nehézségi szint szerint">
          <option value="Összes">Összes</option>
          <option value="Könnyű">Könnyű</option>
          <option value="Közepes">Közepes</option>
          <option value="Nehéz">Nehéz</option>
        </select>
      </div>
      <div v-for="kartya in filteredKartyak" :key="kartya.id" class="mb-3">
        <Kartya :kartya="kartya" @delete-kartya="deleteKartya" @edit-kartya="editKartya" />
      </div>
    </div>
  </div>
</template>

<script>
import KartyaForm from './components/KartyaForm.vue';
import Kartya from './components/Kartya.vue';

export default {
  components: { KartyaForm, Kartya },
  data() {
    return {
      kartyak: [],
      filterDifficulty: 'Összes',
      currentEditKartya: null,
    };
  },
  computed: {
    filteredKartyak() {
      if (this.filterDifficulty === 'Összes') return this.kartyak;
      return this.kartyak.filter(kartya => kartya.nehézség === this.filterDifficulty);
    },
  },
  methods: {
    addKartya(kartya) {
      this.kartyak.push({ ...kartya, id: Date.now() });
    },
    deleteKartya(id) {
      this.kartyak = this.kartyak.filter(kartya => kartya.id !== id);
    },
    editKartya(kartya) {
      this.currentEditKartya = { ...kartya }; // Pass a copy to avoid direct mutation
    },
    updateKartya(updatedKartya) {
      const index = this.kartyak.findIndex(k => k.id === updatedKartya.id);
      if (index !== -1) {
        this.kartyak.splice(index, 1, updatedKartya);
      }
      this.clearEdit();
    },
    clearEdit() {
      this.currentEditKartya = null;
    },
  },
};
</script>
