<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5">
                    <carousel class="product-slider" :items="3" :nav="false" :autoplay="false" :dots="false">
                        <div class="product-item">
                            <div class="pi-pic">
                                <img src="img/mickey1.jpg" alt="" />
                                <ul>
                                    <li class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view">
                                        <router-link to="/product">+ Quick View</router-link> <!-- pengganti a href -->
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">Coat</div>
                                <router-link to="/product">
                                    <h5>Mickey Baggyy</h5>
                                </router-link>
                                <div class="product-price">
                                    $14.00
                                    <span>$35.00</span>
                                </div>
                            </div>
                        </div>
                    </carousel>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel'

export default{
    name: 'WomenShayna',
    components : {
        carousel
    }
}
</script>


<style scoped>
.product-item {
    margin-right: 25px;
}
</style>
