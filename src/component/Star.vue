<script setup>
import { StarIcon } from "@heroicons/vue/24/solid";

const props = defineProps({
    rating: null
});

</script>
<template>
    <section class="star-wrapper">
        <section class="star-icon">
        <StarIcon/>
        <span class="rating">{{ rating }}</span>
    </section>
    </section>
</template>
<style>
.star-wrapper {
    position: absolute;
    right: 10px;
    top: 10px;
}
.star-icon{
    position: relative;
    color: yellow;
    width: 50px;
    height: 50px;
    z-index: 0;
}
.star-icon .rating {
    color: black;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 1;
}
</style>