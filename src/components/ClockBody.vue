<template>
    <div v-if="pageIsLoading">
        <p>Page is loading...</p>
    </div>
    <div v-else :class="morning ? 'morningDiv' : 'eveningDiv'">

        <div class="quote-and-clock">

            <quote-body v-if="!details"></quote-body>

            <div class="main-content">

                <div class="container-for-text">

                    <greeting-body :beforenoon=this.beforenoon :afternoon=this.afternoon :evening=this.evening>
                    </greeting-body>



                    <h1> {{ currentTime }}</h1>
                    <span id="abbreviation"> {{ abbreviation }}</span>
                    <h3> {{ 'IN ' + city + ', ' + country }}</h3>
                </div>


                <div class="container-for-button">
                    <button-body @click="showDetails" :details=this.details></button-body>
                </div>

            </div>

        </div>


        <div class="container" v-if="details">
            <div id="details" v-if="details" :class="morning ? 'morning-details' : 'evening-details'">


                <div class="timezone-details">
                    <h6>Current Timezone</h6>
                    <h2> {{ timezone }}</h2>
                    <h6>Day of the Year</h6>
                    <h2> {{ dayOfTheYear }}</h2>
                </div>

                <div class="week-details">
                    <h6>Day of the week</h6>
                    <h2> {{ dayOfTheWeek }}</h2>
                    <h6>Week number</h6>
                    <h2> {{ weekNumber }}</h2>
                </div>
            </div>
        </div>



    </div>
</template>

<script>
import axios from 'axios';
import QuoteBody from './QuoteBody.vue';
import GreetingBody from './GreetingBody.vue';
import ButtonBody from './ButtonBody.vue';


export default {

    components: {
        QuoteBody,
        GreetingBody,
        ButtonBody,

    },


    data() {
        return {
            pageIsLoading: false,
            error: null,
            abbreviation: "",
            currentTime: "",
            country: "",
            city: "",
            timezone: "",
            dayOfTheWeek: "",
            dayOfTheYear: "",
            weekNumber: "",
            morning: "",
            details: false,
            beforenoon: "",
            afternoon: "",
            evening: "",
        }
    },

    computed: {


    },


    methods: {
        async getData() {
            this.pageIsLoading = true;
            try {
                await axios.get('https://api.ipbase.com/v2/info', {
                    headers: {
                        "X-Api-Key": 'ipb_live_rra6T120SxztDWPZAM1xjpxOOLGCxFDekpg9kskN'
                    },
                })
                    .then((response) => {
                        this.country = response.data.data.location.country.fips;
                        this.city = response.data.data.location.city.name;
                    });
            }
            catch (error) {
                this.error = error.message || 'Something went wrong!'
            }
            this.pageIsLoading = false;

        },

        async getTimeIP() {
            this.pageIsLoading = true;
            try {
                await axios.get('https://worldtimeapi.org/api/ip')
                    .then((response) => {
                        this.abbreviation = response.data.abbreviation
                        this.currentTime = response.data.datetime.slice(11, 16);
                        this.timezone = response.data.timezone;
                        this.dayOfTheWeek = response.data.day_of_week;
                        this.dayOfTheYear = response.data.day_of_year;
                        this.weekNumber = response.data.week_number;
                    })
            }
            catch (error) {
                this.error = error.message || 'Something went wrong!'
            }
            this.pageIsLoading = false;


        },



        checkMorning() {
            const time = this.currentTime;
            const timeInNumber = parseInt(time, 10);

            if (timeInNumber >= 5 && timeInNumber < 18) {
                this.morning = true;
            } else {
                this.morning = false;
            }
        },

        showDetails() {
            this.details = !this.details;
        },


        checkGreeting() {
            const day = this.currentTime;
            const dayInNumber = parseInt(day, 10);

            if (dayInNumber >= 5 && dayInNumber < 12) {
                this.beforenoon = true;
                this.afternoon = false;
                this.evening = false;
            }

            else if (dayInNumber >= 12 && dayInNumber < 18) {
                this.beforenoon = false;
                this.afternoon = true;
                this.evening = false;
            }

            else {
                this.beforenoon = false;
                this.afternoon = false;
                this.evening = true;
            }

        }

    },



    async created() {
        await this.getData();
        await this.getTimeIP();
        this.checkMorning();
        this.checkGreeting();
    },

    mounted() {
        window.setInterval(() => {
            this.getTimeIP();
            this.checkMorning();
            this.checkGreeting();
        }, 60000)
    }



}





</script>

<style scoped>
.morningDiv {
    background-image: linear-gradient(rgba(0, 0, 0, 0.527), rgba(0, 0, 0, 0.295)), url('../assets/assets/desktop/bg-image-daytime.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    height: 1080px;
}

.eveningDiv {
    background-image: url(../assets/assets/desktop/bg-image-nighttime-2.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-attachment: fixed;
    height: 1080px;
}

.quote-and-clock {
    padding: 1% 10% 5% 10%;
}

.main-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
}

h1 {
    display: inline-block;
}


#abbreviation {
    width: 7%;
    display: inline-block;
    font-size: 40px;
    font-weight: 300;
    margin-left: 35px;
}

.container-for-button {
    display: flex;
    width: 100%;
    text-align: end;
    align-items: flex-end;
    flex-direction: row-reverse;
    padding-bottom: 24px;
}

.spaceing {
    padding: 10%;

}

.container {
    width: 100%;
    position: fixed;
    bottom: -100%;
    opacity: 0;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 10px;
    animation: smooth-appear 1s ease forwards;
    backdrop-filter: blur(8px);
}

@keyframes smooth-appear {
    to {
        bottom: 20px;
        opacity: 1;
    }
}

#details {
    height: 400px;
    padding: 1% 10% 2% 10%;
    display: grid;
    grid-template-columns: 1fr 1fr;

}


.morning-details {
    background-color: rgba(255, 255, 255, 0.65);

}

.morning-details h6 {
    color: black;
}

.morning-details h2 {
    color: black;
}

.evening-details {
    background-color: rgba(12, 12, 12, 0.85);
}


@media screen and (max-width: 1400px) {
    .quote-and-clock {
        padding: 1% 10% 3% 10%;
    }

    #details{
      height: 320px;
    }
    .container {
        height: 320px;
    }
    
    .morningDiv,
    .eveningDiv{
        height: 850px;
    }

}

@media screen and (max-width: 820px) {

    #abbreviation {
        font-size: 32px;
    }

    .quote-and-clock {
        padding: 12% 5% 3% 5%;
    }

    .main-content {
        margin-top: 100px;
        grid-template-columns: 1fr;
        grid-template-rows: 2fr 1fr;
        width: 80%;
    }

    .container-for-button {
        flex-direction: row;
    }

    .morningDiv {
        background-image: linear-gradient(rgba(0, 0, 0, 0.527), rgba(0, 0, 0, 0.295)), url('../assets/assets/tablet/bg-image-daytime.jpg');
        height: 1370px;
    }

    .eveningDiv {
        background-image: linear-gradient(rgba(0, 0, 0, 0.527), rgba(0, 0, 0, 0.295)), url(../assets/assets/tablet/bg-image-nighttime.jpg);
        height: 1370px;
    }

    #details {
        grid-column-gap: 25px;
    }

}

@media screen and (max-width: 450px) {

    .main-content {
        width: 100%;
        margin-top: 20px;
    }

    .morningDiv {
        background-image: linear-gradient(rgba(0, 0, 0, 0.527), rgba(0, 0, 0, 0.295)), url('../assets/assets/mobile/bg-image-daytime.jpg');
        max-height: 920px;
    }

    .eveningDiv {
        background-image: linear-gradient(rgba(0, 0, 0, 0.527), rgba(0, 0, 0, 0.295)), url(../assets/assets/mobile/bg-image-nighttime.jpg);
        max-height: 920px;
    }

    .container {
        height: auto;
    }

    #details {
        padding: 1% 5% 2% 5%;
        grid-template-columns: 1fr;
        grid-template-rows: repeat(2, 1fr);
        grid-column-gap: 25px;
        height: 250px;
    }

    #abbreviation{
        font-size: 15px;
    }

    .timezone-details,
    .week-details {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 1fr 1fr;
        align-items: center;
    }


}
</style>