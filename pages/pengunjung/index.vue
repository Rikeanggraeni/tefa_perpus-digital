<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter...">
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table">
          <thead>
            <tr>
              <td>no</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitor" :key="i">
              <td>{{ i + 1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <nuxt-link to="../pengunjung/tambah"><button type="submit"
          class="btn btn-lg rounded-5 px-5 bg-secondary text-white" style="float: right">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const visitors = ref([]);

const pengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select("*, keanggotaan(*), keperluan(*)");
  if (data) visitors.value = data;

  onMounted(() => {
    getPengunjung();
  })
};
</script>
