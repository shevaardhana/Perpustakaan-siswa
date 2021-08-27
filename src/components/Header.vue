<template>
     <header class="header-section">
        <div class="header-top">
            <div class="container">
                <div class="ht-left">
                    <div class="mail-service">
                        <i class=" fa fa-book"></i> Perpustakaan
                    </div>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="inner-header">
                <div class="row">
                    <div class="col-lg-2 col-md-2">
                        <div class="logo">
                            <a href="./index.html">
                                <h5>Selamat Datang Di Perpustakaan</h5>
                            </a>
                        </div>
                    </div>
                    <div class="col-lg-7 col-md-7"></div>
                    <div class="col-lg-3 text-right col-md-3">
                        <ul class="nav-right">
                            <li class="cart-icon">
                                Keranjang Buku &nbsp;
                                <a href="#">
                                    <i class="icon_book_alt"></i>
                                    <span>{{ keranjangBuku.length }}</span>
                                </a>
                                <div class="cart-hover">
                                    <div class="select-items">
                                        <table>
                                            <tbody v-if="keranjangBuku.length > 0">

                                                <tr v-for="keranjang in keranjangBuku" :key="keranjang.id">
                                                    <td class="si-pic">
                                                        <img :src="keranjang.photo" alt="" />
                                                    </td>
                                                    <td class="si-text">
                                                        <div class="product-selected">
                                                            <h6 class="text-warning">{{keranjang.judul}}</h6>
                                                        </div>
                                                    </td>
                                                    <td @click="removeItem(keranjang.id)" class="si-close">
                                                        <i class="ti-close"></i>
                                                    </td>
                                                </tr>
                                            </tbody>

                                            <tbody v-else>
                                                <tr>
                                                    <td>Keranjang Kosong</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </div>
                                    <div class="select-button">
                                        <a href="/ambil-buku" class="primary-btn checkout-btn">TAKE</a>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
export default {
  name: 'Header',
  data(){
      return{
          keranjangBuku : []
      }
  },
  methods:{
      removeItem(idx){
        let kerangjangStorage = JSON.parse(localStorage.getItem("keranjangBuku"));
        let itemKeranjangStorage = kerangjangStorage.map(itemKeranjangStorage => itemKeranjangStorage.id);
        
        let index = itemKeranjangStorage.findIndex(id => id == idx);
        this.keranjangBuku.splice(index, 1);

        const parsed = JSON.stringify(this.keranjangBuku);
        localStorage.setItem("keranjangBuku", parsed);
        window.location.reload();
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
    width: 70px;
    height: 80px;
}
</style>
