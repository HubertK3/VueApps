<template>
  <button @click="showMessage">Kliknij</button>
</template>

<script>
export default {
  methods: {
    showMessage() {
      alert('Nic nie robie :D');
    },
  },
};
</script>