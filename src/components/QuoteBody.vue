<template>
    <section>
        <div v-if="isLoading">
            <p>Page is loading...</p>
        </div>
        <div v-else>
    <h5> {{ quote.content }}</h5>
    <h5 id="author"> {{ quote.author }}</h5>
</div>
    <div @click="getNewQuote()">
    <img src="../assets/assets/desktop/icon-refresh.svg" alt="refresh button" >
</div>
    </section>
</template>


<script>
import axios from 'axios';
export default {

data(){
    return {
       quote: {},
       isLoading: false,
       error: null
    }
    
},

methods: {
    async getNewQuote(){
        this.isLoading = true;
        try {
        await axios.get('https://api.quotable.io/random')
        .then((response) => {
            this.quote = response.data
        });
    }
    catch (error){
        this.error = error.message || 'Something went wrong!';
    }
    this.isLoading = false;
},
},


   mounted(){
    this.getNewQuote()        
    }

}


</script>

<style scoped>

section {
    width: 45%;
    height: 400px;
    display: grid;
    grid-template-columns: 9fr 1fr;
    align-items: baseline;
}

#author{
    font-weight: 700;
}

img{
    padding-left: 10px;
}

img:hover{
    cursor: pointer;
}

@media screen and (max-width: 1500px) {

    section{
        height: 250px;
        width: 60%
    }

}


@media  screen and (max-width: 800px) {

section{
    height: 300px;
    width: 100%;
    height: 200px;
}

}

@media  screen and (max-width: 800px) {

    section{
    height: 300px;
    width: 80%;
    }
}

@media  screen and (max-width: 450px) { 


    section{
    height: 180px;
    width: 100%;
    margin-bottom: 150px;
    }
}



</style>