<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <div class="my-3">
          <form @submit.prevent="getrambuu">
            <input v-model="keyword" type="search" class="form-control rounded-5"
              placeholder="melihat rambu rambu?" />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan edukasi {{ rambu?.length }} dari {{ totalrambuu }}</div>
        <div class="row justify-content-evenly">
          <div v-for="(rambuu, i) in rambu" :key="i" class="col-lg-2">
            <nuxt-link :to="`/rambuu/${rambuu.id}`">
              <div class="card mb-3 shadow-lg">
                <div class="card-body">
                  <img :src="rambuu.cover" class="cover" :alt="rambuu.judul" />
                </div>
              </div>
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </div>
  <nuxt-link to="/">
    <button type="submit" class="btn btn-light btn-lg rounded-5 px-5">BACK</button>
  </nuxt-link>
</template>

<script setup>
const supabase = useSupabaseClient();
const totalrambuu = ref(0);
const rambu = ref([])

const getrambuu = async () => {
  const { data, error } = await supabase
    .from('rambuu')
    .select(`*`)
    .ilike("judul", `%${keyword.value}%`);
  if (error) throw error
  if (data) rambu.value = data;

};
const getTotalRambu = async () => {
  const { count, error } = await supabase.from("rambuu").select("*", { count: 'exact', head: true });
  if (error) throw error
  if (count) totalrambu.value = count;
};

onMounted(() => {
  getrambuu();
  getTotalRambu();
});

const keyword = ref("");
</script>

<style scoped>
.shadow-lg {
  box-shadow: 6px 4px 0 #2e2e2eae !important;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 4px 4px 20px #2e2e2eae !important;
}

.card {
  transition: all .2s ease-in-out;
}

.card-body {
  width: 100%;
  height: 100%;
  padding: 0;
}

.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}

.form-control {
  background-color: #D9D9D9;
}

.btn {
  background-color: #D9D9D9;
}
</style>