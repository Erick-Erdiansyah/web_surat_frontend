<script>
import WelcomeItem from './WelcomeItem.vue';
import IconCommunity from './icons/IconCommunity.vue';

export default {
  components: {
    WelcomeItem,
    IconCommunity,
  }
}
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <IconCommunity />
    </template>
    <template #heading>Tentang</template>
    <h1>hello, ini adalah demo api untuk aplikasi yang kami buat, untuk mengecek fitur lengkapnya
      silahkan click link ini <a href="https://astek.up.railway.app">[astek]</a> untuk dokumentasi lengkap api akan
      menyusul
    </h1>
  </WelcomeItem>
</template>
