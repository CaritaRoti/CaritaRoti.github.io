<template>
  <div>
    <button
      @click="toggleAccordion()"
      :aria-expanded="isOpen"
      :aria-controls="`collapse${_uid}`">
        <slot name="title" />
    </button>

    <div v-show="isOpen" :id="`collapse${_uid}`">
      <slot name="content" />
    </div>
  </div>
</template>
  
<script>
export default {
  name: 'CuriosityAccordion',
  data() {
    return {
      isOpen: false,
    };
  },

  methods: {
    toggleAccordion() {
      this.isOpen = !this.isOpen;
    }
  },
};
</script>

<style>
  span {
    color: white;
  }
</style>