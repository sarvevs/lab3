<template>
  <div id="app">
    <div class="table-body">
      <RecycleScroller class="table" :items="filteredPhotos" item-height="75">
        <div v-for="(photo, index) in filteredPhotos" :key="photo.id" class="table-row">
          <div class="table-cell"><a :href="photo.url" target="_blank">Thumbnail</a></div>
          <div class="table-cell"><img :src="photo.url" @click="showImage(index)"  alt="#"/></div>
          <div class="table-cell">{{ photo.id }}</div>
          <div class="table-cell">{{ photo.title }}</div>
        </div>
      </RecycleScroller>
    </div>
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <img :src="selectedPhoto.url"  alt="#"/>
        <button @click="closeModal">Close</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  components: {
  },
  data() {
    return {
      photos: [],
      selectedPhoto: null,
      showModal: false,
    }
  },
  computed: {
    filteredPhotos() {
      return this.photos.filter((photo) => {
        return photo.title.split(' ').length <= 7

      })
    },
  },
  methods: {
    async fetchPhotos() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/photos')
        this.photos = await response.json()
      } catch (error) {
        console.error(error)
      }
    },
    showImage(index) {
      this.selectedPhoto = this.filteredPhotos[index]
      this.showModal = true
    },
    closeModal() {
      this.showModal = false
    },
  },
  mounted() {
    this.fetchPhotos()

  }
  // created() {
  //   this.fetchPhotos()
  // },
}
</script>

<style>
.table {
  display: table;
  width: 50%;
  border-collapse: collapse;
}
.table img{
  width: 100px;
  height: 100px;
}
.table-row {
  display: table-row;
  height: 25px;
}

.table-cell {
  display: table-cell;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  position: relative;
  width: 80%;
  max-width: 800px;
  background-color: #fff;
  padding: 20px;
  text-align: center;
}

.modal img {
  max-width: 100%;
  height: 100%;
}

</style>
