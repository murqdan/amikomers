<template>
  <div class="page-success">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Terima Kasih</h1>

        <p>Pesanan anda akan diproses dalam waktu 48 jam</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Success',
  mounted() {
    document.title = 'Sukses | Amikomers.';
  },
};
</script>
