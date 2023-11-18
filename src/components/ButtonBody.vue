<template>

<section>
<div class="button-body" v-if="!details">
    <p>More</p>
    <div class="img-body">
        <img id="details-arrow-down" src="../assets/assets/desktop/icon-arrow-down.svg"
            alt="details-arrow-down">
    </div>
</div>

<div class="button-body" v-else>
    <p>Less</p>
    <div class="img-body">
        <img id="details-arrow-up" src="../assets/assets/desktop/icon-arrow-up.svg "
            alt="details-arrow-up">
    </div>
</div>
</section>
</template>

<script>
export default{

    props: ['details']

}


</script>

<style scoped>

.button-body {
    display: flex;
    background-color: white;
    width: 146px;
    height: 56px;
    border-radius: 25px;
    color: black;
    align-items: center;
    justify-content: center;
}

.button-body:hover {
    cursor: pointer;
}

.img-body {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    border-radius: 35px;
    height: 35px;
    width: 35px;
    background-color: #303030;
}

.img-body:hover{
    background-color: #999999;
}

#details-arrow-down {
    align-self: center;
    width: 15px;
    height: 10px;
}

#details-arrow-up {
    align-self: center;
    width: 35px;
    height: 30px;
}



p {
    font-size: 16px;
    text-transform: uppercase;
    color: #303030;
    font-weight: 700;
    letter-spacing: 5px;
    padding-right: 5px;
}




</style>