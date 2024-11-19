<template>
  <div class="card">
    <div class="card-body">
      <h5>{{ kartyaToEdit ? "Kártya szerkesztése" : "Új kártya hozzáadása" }}</h5>
      <div class="mb-2">
        <label>Kérdés</label>
        <input v-model="kerdes" type="text" class="form-control" />
      </div>
      <div class="mb-2">
        <label>Válasz</label>
        <input v-model="valasz" type="text" class="form-control" />
      </div>
      <div class="mb-2">
        <label>Nehézség</label>
        <select v-model="nehézség" class="form-select">
          <option value="Könnyű">Könnyű</option>
          <option value="Közepes">Közepes</option>
          <option value="Nehéz">Nehéz</option>
        </select>
      </div>
      <button
        @click="handleSubmit"
        class="btn btn-primary"
      >
        {{ kartyaToEdit ? "Mentés" : "Hozzáadás" }}
      </button>
      <button
        v-if="kartyaToEdit"
        @click="clearEdit"
        class="btn btn-secondary ms-2"
      >
        Mégse
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    kartyaToEdit: Object, // The card currently being edited
  },
  data() {
    return {
      kerdes: "",
      valasz: "",
      nehézség: "Könnyű",
    };
  },
  watch: {
    kartyaToEdit: {
      immediate: true,
      handler(newVal) {
        if (newVal) {
          this.kerdes = newVal.kerdes;
          this.valasz = newVal.valasz;
          this.nehézség = newVal.nehézség;
        } else {
          this.resetForm();
        }
      },
    },
  },
  methods: {
    handleSubmit() {
      if (this.kerdes && this.valasz) {
        if (this.kartyaToEdit) {
          // Emit update-kartya event if editing
          this.$emit("update-kartya", {
            id: this.kartyaToEdit.id,
            kerdes: this.kerdes,
            valasz: this.valasz,
            nehézség: this.nehézség,
          });
        } else {
          // Emit add-kartya event if adding
          this.$emit("add-kartya", {
            kerdes: this.kerdes,
            valasz: this.valasz,
            nehézség: this.nehézség,
          });
        }
        this.resetForm();
      }
    },
    clearEdit() {
      this.$emit("clear-edit");
      this.resetForm();
    },
    resetForm() {
      this.kerdes = "";
      this.valasz = "";
      this.nehézség = "Könnyű";
    },
  },
};
</script>
