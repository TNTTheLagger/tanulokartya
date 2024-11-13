<template>
  <div class="card p-3">
    <div class="card-content">
      <p :class="{ 'text-muted': showAnswer }">{{ showAnswer ? kartya.valasz : kartya.kerdes }}</p>
    </div>
    <div class="button-group mt-2">
      <button
        @click="toggleLearned"
        :class="learned ? 'btn btn-success' : 'btn btn-secondary'"
      >
        {{ learned ? 'Váltás nem megtanultra' : 'Váltás megtanultra' }}
      </button>
      <button @click="toggleAnswer" class="btn btn-secondary">Mutat válasz</button>
      <button @click="$emit('edit-kartya', kartya)" class="btn btn-primary ms-2">Szerkesztés</button>
      <button @click="$emit('delete-kartya', kartya.id)" class="btn btn-danger ms-2">Törlés</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    kartya: Object,
  },
  data() {
    return {
      learned: false,
      showAnswer: false,
    };
  },
  methods: {
    toggleLearned() {
      this.learned = !this.learned;
    },
    toggleAnswer() {
      this.showAnswer = !this.showAnswer;
    },
  },
};
</script>

<style scoped>
.card {
  background-color: #f8f9fa;
  margin-bottom: 1rem;
}
.text-muted {
  color: gray;
}
.button-group {
  display: flex;
  gap: 8px;
}
</style>
