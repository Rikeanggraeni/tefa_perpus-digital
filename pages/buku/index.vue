<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">BUKU</h2>
        <div class="my-3">
          <form @submit.prevent="getBooks">
            <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Mau baca apa hari ini?">
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan 3 dari 3</div>
        <div class="row">
          <div V-for="(book, i) in books" :key="i" class="col-lg-2">
            <div class="card mb-3">
              <div class="card-body">
                <nuxt-link to="/buku/buku1">
                  <img src="~/assets/img/cover1.jpg" class="cover" alt="cover 1">
                </nuxt-link>
              </div>
            </div>
          </div>
          <div class="col-lg-2">
            <div class="card mb-3">
              <div class="card-body">
                <nuxt-link to="/buku/buku2">
                  <img src="~/assets/img/cover2.jpg" class="cover" alt="cover 2">
                </nuxt-link>
              </div>
            </div>
          </div>
          <div class="col-lg-2">
            <div class="card mb-3">
              <div class="card-body">
                <nuxt-link to="/buku/buku3">
                  <img src="~/assets/img/cover3.jpg" class="cover" alt="cover 3">
                </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
      <nuxt-link to="../"><button type="submit" class="btn btn-secondary btn-lg rounded-5 px-5"
          style="margin-left: 82.5%;">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const books = ref([])

const getBooks = async () => {
  const { data, error } = await supabase.from('buku').select('*, kategori(*')
    .ilike('judul', '%${keyword.value}%')
  if (data) books.value = data
}

onMounted(() => {
  getBooks()
})
</script>

<style scoped>
.card-body {
  width: 100%;
  height: 30em;
  padding: 0;
}

.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}
</style>
