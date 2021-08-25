<template>
  <div>
    <Header />
    <BreadCrumb />

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="bookDetail.photo" alt="" />
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details">
                                <div class="pd-title text-left">
                                    <span>{{bookDetail.category.kategori}}</span>
                                    <h3>{{bookDetail.judul}}</h3>
                                </div>
                                <div class="pd-desc text-left">
                                    <p v-html="bookDetail.deskripsi"></p>
                                </div>
                                <div class="quantity">
                                    <a @click="saveKeranjang(bookDetail.id, bookDetail.judul, bookDetail.photo)" href="#" class="primary-btn pd-cart mr-2">Tambah Ke keranjang</a>
                                </div>
                                
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import BreadCrumb from '@/components/BreadCrumb.vue'
import axios from 'axios'

export default {
  name: 'Book',
  components: {
    Header,
    BreadCrumb
  },
  data(){
      return{
          bookDetail : [],
          keranjangBuku : []
      }
  },

methods:{
    saveKeranjang(idBuku, judulBuku, photoBuku){

        var bookStored = {
            "id" : idBuku,
            "judul" : judulBuku,
            "photo" : photoBuku,
        }

        this.keranjangBuku.push(bookStored);
        const parsed = JSON.stringify(this.keranjangBuku);
        localStorage.setItem('keranjangBuku', parsed);

        window.location.href = '/'
    }
  },

  mounted(){
      if(localStorage.getItem('keranjangBuku')){
          try{
            this.keranjangBuku = JSON.parse(localStorage.getItem('keranjangBuku'));
          }
          
          catch(e){
              localStorage.removeItem('keranjangBuku');
          }
      }

      axios
        .get("http://127.0.0.1:8000/api/books", {
            params : {
                id: this.$route.params.id
            }
        })
        .then(res => (this.bookDetail = res.data.data))
        .catch(err => console.log(err));
  }
}
</script>