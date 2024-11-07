<template>
    <div>
        <h2 class="text-start my-4">{{ rambuu.judul }}</h2>
        <div class="row">
            <div class="col-md-3">
                <div class="card">
                    <div class="card-body">
                        <span v-if="rambuu.cover"><img class="cover" :src="rambuu.cover" :alt="rambuu.judul"></span>
                <span v-else><img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE" class="cover"></span>
                    </div>
                </div>
            </div>
            <div class="col-md-6">
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">jenis rambu : {{  rambuu.judul }}</li>
                    <li class="list-group-item">keterangan : {{  rambuu.keterangan }}</li>
                </ul>
            </div>
        </div>
        <NuxtLink to="/rambuu" class="btn btn-light btn-lg rounded-5 px-5">
         kembali
        </NuxtLink>
    </div>
</template>

<script setup>
import { onMounted } from 'vue';

const supabase = useSupabaseClient()
const route = useRoute()
const rambuu = ref([])

const getrambuuByID = async () => {
    const { data, error } = await supabase
    .from('rambuu')
    .select(`*`)
    .eq('id', route.params.id)
    .single()
    if(data) rambuu.value = data
}

onMounted(() => {
    getrambuuByID()
})
</script>
<style scoped>
.cover{
    width: 100%;
}
</style>