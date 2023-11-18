<template>
    <div class="img-and-greeting">

<div class="beforenoon" v-if="beforenoon">
    <img src="../assets/assets/desktop/icon-sun.svg" alt="sun-icon">
    <h4>
        Good morning, it's currently
    </h4>
</div>

<div class="afternoon" v-if="afternoon">
    <img src="../assets/assets/desktop/icon-sun.svg" alt="sun-icon">
    <h4>
        Good afternoon, it's currently
    </h4>
</div>

<div class="evening" v-if="evening">
    <img src="../assets/assets/desktop/icon-moon.svg" alt="moon-icon">
    <h4>
        Good evening, it's currently
    </h4>
</div>
</div>
</template>

<script>

export default {
    props: ['beforenoon', 'afternoon', 'evening']

}

</script>

<style scoped>
.beforenoon,
.afternoon,
.evening {
    display: grid;
    grid-template-columns: 1fr 10fr;
    align-items: center;
}
</style>