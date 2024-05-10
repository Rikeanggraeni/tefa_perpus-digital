<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <from @submit.prevent="getpengunjung">
          <input type="search" class="form-control form-control-lg rounded-5" placeholder="filter...">
          </from>
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table tabel-bordered">
          <thead>
            <tr align="center">
              <td>NO</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitors,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitors.nama }}</td>
              <td>{{ visitors.keanggotaan.nama }}</td>
              <td>{{ visitors.tanggal }},{{ visitors.waktu }}</td>
              <td>{{ visitors.keperluaan.nama }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <nuxt-link to="../pengunjung/tambah"><button type="submit" class="btn btn-lg btn-dark rounded-5 px-5 bg-primary text-white" style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const visitors  = ref([]);

const getpengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select(', keanggotaan(), keperluan(*)');
  if(data) visitors.value = data
}

onMounted (() => {
  getpengunjung()
})
</script>