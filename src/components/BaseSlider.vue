<script>
export default {
  props: ["image"],
};
</script>

<template>
  <div>
    <div class="slider-item">
      <img :src="image" alt="image" />
    </div>
  </div>
</template>

<style>
.slider-item {
  height: 100px;
}
</style>