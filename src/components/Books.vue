<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">

                <div class="col-lg-3 mt-5" v-for="itemBook in books" v-bind:key="itemBook.id">
                    <div class="product-item">
                        <div class="pi-pic">
                            <img v-bind:src="itemBook.photo" />
                            <ul>
                                <li class="w-icon active">
                                    <a @click="saveKeranjang(itemBook.id, itemBook.judul, itemBook.photo)" href="#"><i class="fa fa-plus"></i></a>
                                </li>
                                <li class="quick-view"><router-link v-bind:to="'/buku/'+itemBook.id">+ Deskripsi</router-link></li>
                            </ul>
                            <h5>{{itemBook.judul}}</h5>
                            <span class="badge badge-secondary">{{itemBook.category.kategori}}</span>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import axios from "axios";
export default {
  name: 'Book',
  data(){
      return{
          books : [],
          keranjangBuku : []
      };
  },

methods:{
    saveKeranjang(idBuku, judulBuku, photoBuku){

        var bookStored = {
            "id" : idBuku,
            "judul" : judulBuku,
            "photo" : photoBuku
        }

        this.keranjangBuku.push(bookStored);
        const parsed = JSON.stringify(this.keranjangBuku);
        localStorage.setItem('keranjangBuku', parsed);
    }
  },

  mounted(){
      axios
        .get("http://127.0.0.1:8000/api/books")
        .then(res => (this.books = res.data.data.data))

        .catch(err => console.log(err));
  }
}
</script>

<style scoped>
img{
    height: 500px;
    width:300px;
}
</style>