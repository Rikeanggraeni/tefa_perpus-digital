<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
        <form>
          <div class="mb-3">
            <input type="text" class="form-control form-control-lg rounded-5" placeholder="NAMA...">
          </div>
          <div class="mb-3">
            <select v-model="form.keanggotaan">
              <option value="">keanggotaan</option>
              <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
            </select>
          </div>
          <div class="mb-3">
            <div class="row">
              <div class="col-md-4">
                <select class="form-control form-control-lg rounded-5">
                  <option value="">TINGKAT</option>
                  <option value="X">X</option>
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>
                </select>
              </div>
              <div class="col-md-4">
                <select class="form-control form-control-lg rounded-5">
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                </select>
              </div>
              <div class="col-md-4">
                <select class="form-control form-control-lg rounded-5">
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <select v-model="form.keperluan">
              <option value="">KEPERLUAN</option>
              <option v-for="(item, i) in objectivies" :key="i" :value="item.id">{{ item.nama }}</option>
            </select>
          </div>
          <nuxt-link to="../pengunjung">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5 bg-secondary">KIRIM</button>
          </nuxt-link>
          <nuxt-link to="../">
            <button type="submit" class="btn btn-lg rounded-5 px-5 bg-secondary text-white"
              style="float: right">KEMBALI</button>
          </nuxt-link>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const members = ref([])
const objectivies = ref([])

const from = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
});

const kirimData = async () => {
  // console.log (form.value)
  const { error } = await supabase.from('pengunjung').insert([form.value])
  if (!error) navigateTo("/pengunjung")
};

const getKeanggotaan = async () => {
  const { data, error } = await supabase.from("keanggotaan").select('*')
  if (data) members.value = data;
};

const getkeperluan = async () => {
  const { data, error } = await supabase.from("keperluan").select('*')
  if (data) objectivies.value = data;
};

onMounted(() => {
  getKeanggotaan()
  getkeperluan()
})
</script>