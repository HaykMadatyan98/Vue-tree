<template>
  <div class="modal">
    <div class="modal-content">
      <h3>{{ title }}</h3>
      <slot />
      <button @click="finish">Ок</button>
      <button @click="close">Закрыть</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  setup(props, { emit }) {
    const close = () => {
      emit("close");
    };

    const finish = () => {
      emit("select");
    };

    return {
      close,
      finish,
    };
  },
});
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
}
</style>
