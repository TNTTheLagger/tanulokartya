<template>
  <div class="card">
    <div class="card-body">
      <h5>Új kártya hozzáadása</h5>
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
      <button @click="addKartya" class="btn btn-primary">Hozzáadás</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      kerdes: "",
      valasz: "",
      nehézség: "Könnyű",
    };
  },
  methods: {
    addKartya() {
      if (this.kerdes && this.valasz) {
        this.$emit("add-kartya", {
          kerdes: this.kerdes,
          valasz: this.valasz,
          nehézség: this.nehézség,
        });
        this.kerdes = "";
        this.valasz = "";
        this.nehézség = "Könnyű";
      }
    },
  },
};
</script>
