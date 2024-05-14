<template>
  <div class="container-fluid">
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-2">
        <span v-if="buku.cover"><img :src="buku.cover" :alt="buku.judul" /></span>
      </div>
      <div class="col-md-4">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
          <li class="list-group-item">Penerbit: {{ buku.penerbit }}</li>
          <li class="list-group-item">Tahun Terbit: {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">deskripsi : {{ buku.deskripsi }}</li>
        </ul>
      </div>
      <nuxt-link to="../buku"><button type="submit" class="btn btn-lg btn-dark rounded-5 px-5 bg-primary text-white"
          style="float: right; margin-bottom: 15px">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const route = useRoute();
const buku = ref([]);

const getBukuByld = async () => {
  const { data, error } = await supabase
    .from("buku")
    .select(`*, kategori(*)`)
    .eq("id", route.params.id)
    .single()
  if (data) buku.value = data;
};

onMounted(() => {
  getBukuByld();
});
</script>

<style scoped>
img {
  width: 100%;
}
</style>