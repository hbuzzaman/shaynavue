<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0" >
                    <!-- carousel -->
                    <carousel class="product-slider" :items="3" :nav="false" :autoplay="false" :dots="false">
                        <!-- mengambil data products(yg ada di bawah) dengan nama itemProduct -->
                        <!-- v-for untuk perulangan mengambil data, dan v bind untuk tiap2 datanya -->
                        <!-- jgn lupa tambahkan props pada router -> index.js -->
                        <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                            <div class="pi-pic">
                                <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                <ul>
                                    <li class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view">
                                        <router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View</router-link> <!-- pengganti a href -->
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{ itemProduct.type}}</div>
                                <router-link to="/product">
                                    <h5>{{ itemProduct.name}}</h5>
                                </router-link>
                                <div class="product-price">
                                    ${{ itemProduct.price}}
                                    <span>$35.00d</span>
                                </div>
                            </div>
                        </div>
                    </carousel>
                </div>

                <div class="col-lg-12" v-else>
                    <p>Produk terbaru belum tersedia</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default{
    name: 'WomenShayna',
    components : {
        carousel
    },
    data(){
        return {
            products: [], //array products untuk menampung data produk yang diambil pada API
            keranjangUser: []
        };
    },
    mounted(){
        axios
            .get("http://shayna-be.test/api/products") //link API
            .then(res=>(this.products = res.data.data.data)) //res=result. menampilkan result data yang dimasukan pada array products. data disini yang SUB keberapa pada API
            .catch(err=>console.log(err));

        if (localStorage.getItem("keranjangUser")) {
            try{
                this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
            } catch (e) {
                localStorage.removeItem("keranjangUser");
            }
        }
    },
    saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct){
        var productStored = {
            id: idProduct,
            name: nameProduct,
            price: priceProduct,
            photo: photoProduct
        };

        this.keranjangUser.push(productStored);
        const parsed = JSON.stringify(this.keranjangUser);
        localStorage.setItem("keranjangUser", parsed);

        window.location.reload();
    }
};
</script>


<style scoped>
.product-item {
    margin-right: 25px;
}
.pi-pic img {
    height: 450px;
}
</style>
