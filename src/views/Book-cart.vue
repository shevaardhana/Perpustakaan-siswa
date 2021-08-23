<template>
  <div>
    <Header />
    <BreadCrumb />

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-12">
                            <div class="cart-table">
                                <table border="1px">
                                    <thead>
                                        <tr>
                                            <th>Image</th>
                                            <th class="p-name text-center">Judul Buku</th>
                                            <th>Jumlah Pinjam</th>
                                            <th>Action</th>
                                        </tr>
                                    </thead>
                                    <tbody>

                                        <tr v-for="keranjang in keranjangBuku" :key="keranjang.id">
                                            <td class="cart-pic first-row">
                                                <img :src="keranjang.photo" alt="" />
                                            </td>
                                            <td class="cart-title first-row text-center">
                                                <h5>{{keranjang.judul}}</h5>
                                            </td>
                                            <td class="p-price first-row"><input type="number" id="jumlah_buku" name="jumlah_buku" placeholder="0"></td>
                                            <td class="delete-item"><a href="#" @click="removeItem(index)"><i class="material-icons">
                                              close
                                              </i></a></td>
                                        </tr>
                                        
                                    </tbody>
                                </table>
                            </div>
                        </div>
                        <div class="col-lg-12">
                            <h4 class="mb-4">
                                Informasi Peminjam:
                            </h4>
                            <div class="user-checkout text-left">
                                <form>
                                    <div class="form-group">
                                        <label for="NIS">NIS</label>
                                        <input type="text" class="form-control" id="no_siswa" aria-describedby="noHelp" placeholder="Masukan NIS">
                                    </div>
                                    <div class="form-group">
                                        <label for="nama">Nama Lengkap</label>
                                        <input type="text" class="form-control" id="nama" aria-describedby="namaHelp" placeholder="Masukan Nama">
                                    </div>
                                    <div class="form-group">
                                        <label for="tanggal_pinjam">Tanggal Pinjam</label>
                                        <input type="date" class="form-control" id="tanggal_pinjam" aria-describedby="tanggal_pinjamHelp">
                                    </div>
                                    <div class="form-group">
                                        <label for="tanggal_pengembalian">Tanggal Pengembalian</label>
                                        <input type="date" class="form-control" id="tanggal_pengembalian" aria-describedby="tanggal_pengembalianHelp">
                                    </div>
                                </form>
                            </div>
                            <button type="submit" href="success.html" class="btn btn-success btn-lg btn-block">Ayo Ambil !!!</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Shopping Cart Section End -->
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import BreadCrumb from '@/components/BreadCrumb.vue'

export default {
  name: 'Book-cart',
  components: {
    Header,
    BreadCrumb
  },
  data(){
      return{
          keranjangBuku : []
      }
  },
  methods:{
      removeItem(index){
        this.keranjangBuku.splice(index, 1);

        const parsed = JSON.stringify(this.keranjangBuku);
        localStorage.setItem('keranjangBuku', parsed);
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
  }
}
</script>
<style scoped>
img{
    width: 120px;
    height: 200px;
}
</style>