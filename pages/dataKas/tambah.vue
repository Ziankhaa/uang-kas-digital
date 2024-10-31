<template> 
  <div class="container-fluid"> 
    <div class="row"> 
      <div class="col-lg-12"> 
        <h2 class="text-center my-4">Bayar Uang Kas Digital PPLG 4</h2>
        <form @submit.prevent="kirimData">
          <div class="row d-flex justify-content-center">
            <div class="mb-3 col-lg-6"> 
              <select v-model="form.nama_siswa" class="form-control form-control-lg form-select rounded-3 mb-2"> 
                <option value="">Nama...</option>
                <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
              </select> 
            </div>
          </div>
          
          <div class="row d-flex justify-content-center">
            <div class="mb-3 col-lg-6">
              <input v-model="form.jumlah" type="number" class="form-control form-control-lg form-select rounded-3 mb-2" placeholder="Nominal Bayar:">
            </div>
          </div>

          <div class="row d-flex justify-content-center">
            <div class="col-lg-6">
                <button type="submit" class="btn btn-success btn-lg rounded-3 px-3"> Kirim </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn-success {
  background-color: #000000;
}

input {
  background: #D9D9D9;
}

select {
  background: #D9D9D9;
}
</style>

<script setup>
import {ref, onMounted} from 'vue'

const supabase = useSupabaseClient()

const members = ref([])

const form = ref({
  nama_siswa: "",
  jumlah: "",
})

const kirimData = async () => {
  console.log(form.value)
  const { data, error } = await supabase
  .from('masuk')
  .insert({
    nama_siswa: form.value.nama_siswa,
    jumlah: form.value.jumlah
  })
  .select()
  if (data) navigateTo('/dataKas/')
}

const getNama = async () => {
  const { data, error } = await supabase.from('siswa').select('id, nama')
  if (error) {
    console.error('Gagal mengambil nama')
    return
  }
  members.value = data
}

onMounted(getNama)
</script>
