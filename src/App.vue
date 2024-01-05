<template>
 
 <clock-body></clock-body>
  
</template>

<script>



import ClockBody from './components/ClockBody.vue';

export default {
    components: {
        ClockBody
    }
}


</script>

   <style>
   @import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&display=swap");
   
   *{
       color: white;
       font-family: 'Inter', sans-serif;
       box-sizing: border-box;
   }
   
   body{
       margin: 0;
   }
   
   h1{ 
       font-size: 200px;
       letter-spacing: -5px;
       font-weight: 700;
       margin: 0;
   }
   
   h2{
       font-size: 56px;
       font-weight: 700;
       line-height: 68px;
   }
   
   h3{
       font-size: 24px;
       font-weight: 700;
       text-transform: uppercase;
       letter-spacing: 4.8px
   }
   
   h4{
       font-size: 20px;
       line-height: 28px;
       letter-spacing: 4px;
       text-transform: uppercase;
       font-weight: 300; 
   }
   
   h5{
       font-size: 18px;
       line-height: 28px;
       font-weight: 500;
   }
   
   h6{
       font-size: 15px;
       font-weight: 700;
       letter-spacing: 3px;
       text-transform: uppercase;
   }
   
   @media screen and (max-width: 1500px) {
       h1{
           font-size: 160px;
       }
   
       h2{
           font-size: 36px;
       }

       h6{
        line-height: 10px;
       }
   }
   

   @media  screen and (max-width: 800px) {
   
       h1{
           font-size: 175px;
           line-height: 180px;
       }
   
       h3{
           font-size: 18px;
           line-height: 20px;
           margin: 5px;
           }
   
       h4{
           font-size: 18px;
           line-height: 20px;
           margin: 5px;
       }
   
       h5{
           font-size: 18px;
       }
   
   }
   
   @media  screen and (max-width: 450px) { 
   
       h1{
           font-size: 100px;
           line-height: 120px;
       }
   
       h2{
           font-size: 18px;
           line-height: 22px;
           text-align: right;
           margin: 0
       }
   
       h4{
           font-size: 15px;
       }
   
       h5{
           font-size: 12px;
       }
   
       h6{
           font-size: 10px;
           font-weight: 500;
           margin: 12px 0;
   
       }
   }
   
   </style>