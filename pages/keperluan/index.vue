<template>
    <div class="countainer-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">RIWAYAT KAS KELUAR</h2>
                <div class="my-3">
                    <input type="search" class="form-control form-control-lg rounded-5" placeholder="Cari...">
                </div>
                <form @submit.prevent="getdataKas">
                <div class="my-3 text-muted"> Menampilkan {{ visitors.length }} dari {{ jumlah }}</div>
                <table class="table">
                    <thead>
                        <tr>
                            <td>NO</td>
                            <td>NAMA</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                            <td>NOMINAL</td>
                        </tr>
                    </thead>
                    <tbody>
                       <tr v-for="(visitor,i) in visitors" :key="i">
                        <td>{{ i+1 }}.</td>
                        <td>{{ visitor.siswa.nama }}</td>
                        <td>{{ visitor.tanggal }}</td>
                        <td>{{ visitor.keperluan }}</td>
                        <td>{{ visitor.nominal }}</td>
                    </tr>
                    </tbody>
                </table>
            </form>
                <nuxt-link to="/">
                    <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kembali</button>
                </nuxt-link>
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref ([])
const jumlah = ref(0)

const getdataKas = async () => {
    const { data, error } = await supabase.from('keluar').select(`*,siswa(nama)`)
    if(data) visitors.value = data
}
const totaldataKas = async () => {
    const {data,count} = await supabase.from('keluar').select('*' , { count:'exact' })
    if (data) jumlah.value = count
}

onMounted(() => {
    getdataKas()
    totaldataKas()
})
</script>