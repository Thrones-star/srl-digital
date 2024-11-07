<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">riwayat penggunaan lab</h2>
                <div class="my-3">
                </div>
                <div class="my-3 text-muted">menampilkan daftar </div>
                 <table class="table">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>NAMA</td>
                            <td>KEANGGOTAAN</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(visitor,i) in visitors" :key="i">
                            <td>{{ i+1 }}.</td>
                            <td>{{ visitor.nama }}</td>
                            <td>{{ visitor.keanggotaan.nama }}</td>
                            <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
                            <td>{{ visitor.keperluan.nama }}</td>
                        </tr>
                    </tbody>
                 </table>
            </div>
        </div>
        <NuxtLink to="/">
            <button class="btn btn-dark btn-lg rounded-5 px-5">BACK</button>
        </NuxtLink>
        <NuxtLink to="/penggunaan_lab/tambah">
            <button class="btn btn-dark btn-lg rounded-5 px-5">ISI KUNJUNGAN</button>
        </NuxtLink>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()
const visitors = ref([]);

const getPengunjung = async () => {
    const { data, error } = await supabase.from('penggunaan_lab').select(`*, keanggotaan(*), keperluan(*)`)
    .order('id', { ascending: false })
    if (error) throw error
    console.log(data)
    if(data) visitors.value = data
}
onMounted(() => {
    getPengunjung();
})
</script>
