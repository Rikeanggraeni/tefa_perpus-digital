<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <form @submit.prevent="cariPengunjung">
            <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Filter" />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan {{ visitors.length }} dari {{ visitors.length }}</div>
        <table class="table">
          <thead>
            <tr align="center">
              <td>NO</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>JURUSAN</td>
              <td>KELAS</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ i + 1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.jurusan }}</td>
              <td>{{ visitor.kelas }}</td>
              <td>{{ visitor.tanggal }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <nuxt-link to="../pengunjung/tambah"><button type="submit"
          class="btn btn-lg btn-dark rounded-5 px-5 bg-primary text-white"
          style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
useHead({ title: "pengunjung perpus" });

import Id from '../buku/[id].vue';

const supabase = useSupabaseClient();

const visitors = ref([]);
const keyword = ref("");

const getpengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung')
    .select(`*, keanggotaan(*), keperluan(*)`).order(`id`, { ascending: false });
  if (data) visitors.value = data;
}


const cariPengunjung = async () => {
  const { data, error } = await supabase
    .from("pengunjung")
    .select(`*, keanggotaan(*), keperluan(*)`)
    .ilike('nama', `%${keyword.value}%`);
  if (data) visitors.value = data;
};


onMounted(() => {
  getpengunjung()
  cariPengunjung()
})
</script>