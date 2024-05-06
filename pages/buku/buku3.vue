<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-2">
        <div class="card mb-3">
          <div class="card-body">
            <img src="assets/img/wherestoriesbegin.jpeg" class="wherestoriesbegin" alt="">
          </div>
        </div>
      </div>
      <div class="col-lg-6">
        <div class="col p-5">
          <h1 style="font-size: 40px;">WHERE STORIES BEGIN</h1>
        </div>
        <h4>Penulis: </h4>
      </div>
    </div>
    <nuxt-link to="../"><button type="submit" class="btn btn-secondary btn-lg rounded-5 px-5"
        style="margin-left: 82.5%;">KEMBALI</button></nuxt-link>
  </div>
</template>


<style scoped>
.cover {
  height: 300px;
  width: 200px;
}

.card.mb-3 {
  margin-top: 50px;
  margin-left: 20px;
  height: 340px;
  width: 235px;
}

h3 {
  margin-top: 60px;
  margin-left: 20px;
}

img {
  height: 300px;
  width: 200px;
}
</style>
