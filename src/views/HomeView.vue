<template>
  <div class="home">
    <HeaderShayna />
    <HeroShayna />
    <WomenShayna />
    <InstaShayna />
    <PartnerShayna />
    <FooterShayna />


  </div>
</template>

<script>
// @ is an alias to /src
import HeaderShayna from '@/components/HeaderShayna.vue'
import HeroShayna from '@/components/HeroShayna.vue'
import WomenShayna from '@/components/WomenShayna.vue'
import InstaShayna from '@/components/InstaShayna.vue'
import PartnerShayna from '@/components/PartnerShayna.vue'
import FooterShayna from '@/components/FooterShayna.vue'
// import carousel from 'vue-owl-carousel' //instal dependencies carousel dengan vue UI

export default {
  name: 'HomeView',
  components: {
    HeaderShayna,
    // carousel, //pindah ke HeroShayna.vue 
    HeroShayna,
    WomenShayna,
    InstaShayna,
    PartnerShayna,
    FooterShayna,
  }
}
</script>
