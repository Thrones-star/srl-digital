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
                            <tr v-for="(alat, i) in alats" :key="alat.id">
                                <td>{{ i + 1 }}</td>
                                <td>{{ alat.nama }}</td>
                                <td>{{ alat.keanggotaan.nama }}</td>
                                <td>{{ alat.tanggal }}, {{ alat.waktu }}</td>
                                <td>{{ alat.keperluan_alat.nama }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
        </div>
        <NuxtLink to="/">
            <button class="btn btn-dark btn-lg rounded-5 px-5">BACK</button>
        </NuxtLink>
        <NuxtLink to="/alat/tambah">
            <button class="btn btn-dark btn-lg rounded-5 px-5">PINJAM ALAT</button>
        </NuxtLink>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const alats = ref([])

async function getAlat() {
    const { data, error } = await supabase.from('penggunaan_alat').select(`
        *,
        keperluan_alat ( nama ),
        keanggotaan ( nama )
    `)
    if (error) throw error
    if (data) alats.value = data
}

onMounted(() => {
    getAlat()
})
</script>