<template>
  <div class="product">
    <HeaderShayna />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        <router-link to="/">
                            <i class="fa fa-home"></i> Home
                        </router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <!-- Binding gambar sesuai data yang ada pada API -->
                                <img class="product-big-img" :src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length>0">
                                <carousel class="product-thumbs-track ps-slider" :nav="false" :dots="false">
                                    <!-- perulangan produk galleri dengan ID produk -->
                                    <div 
                                        v-for="ss in productDetails.galleries" 
                                        :key="ss.id" 
                                        class="pt" 
                                        @click="changeImage(ss.photo)" 
                                        :class="ss.photo == gambar_default ? 'active': '' "
                                        >
                                            <img :src="ss.photo" alt/>
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{productDetails.type}}</span>
                                    <h3>{{productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{productDetails.description}}
                                    </p>
                                    <h4>Rp {{productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedShayna />
    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderShayna from '@/components/HeaderShayna.vue';
import RelatedShayna from '@/components/RelatedShayna.vue';
import FooterShayna from '@/components/FooterShayna.vue';
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default {
  name: 'ProductView',
  components: {
    HeaderShayna,
    RelatedShayna,
    FooterShayna,
    carousel
  },
  data(){
    return{
      gambar_default: "img/mickey1.jpg",
      thumbs: [
        "img/mickey1.jpg",
        "img/mickey2.jpg",
        "img/mickey3.jpg",
        "img/mickey4.jpg"
      ],
      productDetails: []
    }

  },
  methods: {
    changeImage(urlImage){
      this.gambar_default=urlImage;
    },
    setDataPicture(data){
        // mengganti OBJEK productDetails dengan parameter data yang diambil dari API
        this.productDetails=data;
        // menganti value gambar default
        this.gambar_default=data.galleries[0].photo;
    }
  
  },
  mounted(){
        axios
            .get("http://shayna-be.test/api/products", {
                params:{
                    id: this.$route.params.id
                }
            }) //link API dengan parameter ID pada router
            .then(res=>(this.setDataPicture(res.data.data))) //res=result.
            .catch(err=>console.log(err));
  }
};
</script>

<style scoped>
.product-thumbs .pt{
  margin-right: 13px;
}
</style>