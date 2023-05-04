<template>
  <div class="modal-mask" @click="$emit('close')">
    <div class="modal-wrapper">
      <div class="modal-container">
        <div class="modal-header">
          <h3>{{ photo.title }}</h3>
        </div>
        <div class="modal-body">
          <img :src="photo.url" />
        </div>
        <div class="modal-footer">
          <button @click="$emit('close')">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    photo: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style>
.modal-mask {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-wrapper {
  width: 100%;
  max-width: 900px;
  margin: 0 20px;
}

.modal-container {
  background-color: white;
  padding: 20px;
  border-radius: 4px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.modal-body img {
  max-width: 100%;
  height: auto;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}
</style>
