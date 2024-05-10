<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">ISI BUKU kunjungan</h2>
        <form @submit.prevent="kirimData">
          <div class="mb-3">
            <!-- <input type="search" class="form-control form-control-lg rounded-5" placeholder="NAMA.../"> -->
            <input v-model="form.nama" type="text" class="form-control form-control-lg rounded-4" placeholder="NAMA" />
          </div>
          <div class="mb-3">
            <select v-model="form.keanggotaan" class="form-control form-control-lg form-select rounded-5">
              <option value="">KEANGGOTAAN</option>
              <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
            </select>
          </div>
          <div class="mb-3" v-if="form.keanggotaan == '5'">
            <div class="row">
              <div class="col-lg-4">
                <select v-model="form.tingkat" class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">TINGKAT</option>
                  <option value="X">X</option>
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>
                </select>
              </div>
              <div class="col-lg-4">
                <select v-model="form.jurusan" class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                  <option value="TOI">TOI</option>
                </select>
              </div>
              <div class="col-lg-4">
                <select class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">KELAS</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <select v-model="form.keperluan" class="form-control form-control-lg form-select rounded-5">
              <option value="">KEPERLUAN</option>
              <option value="baca buku">baca buku</option>
              <option value="pinjam buku">pinjam buku</option>
              <option value="kembalikan buku">kembalikan buku</option>
              <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
            </select>
          </div>
          <nuxt-link to="../pengunjung"><button type="submit"
              class="btn btn-dark btn-lg rounded-5 px-5 bg-primary">KIRIM</button></nuxt-link>
          <nuxt-link to="../"><button type="submit"
              class="btn btn-light btn-lg  btn-dark rounded-5 px-5 bg-primary text-white"
              style="float: right;">KEMBALI</button></nuxt-link>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const members = ref([]);
const objectives = ref([]);


const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
});


const kirimData = async () => {
  console.log(form.value)
  const { error } = await supabase.from('pengunjung').insert([from.value]);
  if (!error) navigateTo('/pengunjung');
};


const getkeanggotaan = async () => {
  const { data, error } = await supabase.from('keanggotaan').select('*');
  if (data) members.value = data;
};

const getkeperluan = async () => {
  const { data, error } = await supabase.from('keperluaan').select('*');
  if (data) members.value = data;
};

onMounted(() => {
  getkeanggotaan();
  getkeperluan();
});
</script>