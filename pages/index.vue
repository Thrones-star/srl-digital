<template>
    <div class="container-fluid">
        <div class=" row my-5">
            <div class="col-lg-6 box">
                <nuxt-link to="/penggunaan_lab">
                    <div class="card bg-pengunjung rounded-5">
                        <div class="card-body">
                          <div class="textPL">
                            <h2>PENGGUNAAN LAB</h2>
                          </div>
                        </div>
                    </div>
                </nuxt-link>
            </div>
            <div class="col-lg-6 box">
              <nuxt-link to="/alat">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                          <div class="textPL">
                            <h2>PENGGUNAAN ALAT</h2>
                          </div>
                        </div>
                    </div>
                </nuxt-link>
            </div>
            <div class="row">
              <div class="col-md-6 offset-md-3 box"style="padding-top: 50px">
              <nuxt-link to="../rambuu">
                    <div class=" card bg-rambuu rounded-5">
                        <div class="card-body">
                          <div class="textPL">
                            <h2>RAMBU RAMBU</h2>
                          </div>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
    </div>
  </div>
</template>


<script setup>
const supabase = useSupabaseClient()
const jml_pengunjung = ref(0)
const jml_buku = ref(0)

async function getjml_pengunjung() {
  const{ error , data, count } = await supabase
  .from("Pengunjung")
  .select('*', { count: 'exact' })
  if (count) jml_pengunjung.value = count
  
}
async function getjml_buku() {
  const{ error , data, count } = await supabase
  .from("buku")
  .select('*', { count: 'exact' })
  if (count) jml_buku.value = count
  
}


onMounted(() => {
  getjml_pengunjung()
  getjml_buku()
})
</script>

<style scoped>
.card {
    height: 200px;
}
.card.bg-pengunjung {
    background-image: url('../assets/img/ruangan.jpg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
.card.bg-buku {
    background: url('../assets/img/barang.jpg') no-repeat center center;
    background-size: cover;
}
.card.bg-rambuu {
    background: url('../assets/img/rambuu.jpg') no-repeat center center;
    background-size: cover;
    
 
}
.card-body h2{
    color:white;
}
.box {
  width: 50%;
}
.box a{
  text-decoration: none;
}
.textPL{
  padding-top: 135px;
  height: 100px;
}
</style>

