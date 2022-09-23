<template>

    <h2>Countdown</h2> -->
   <div class="clock" v-if="Loading">
        <div>
            <span id="days">{{displayDays}}</span>
            <span class="text">Days</span>
        </div>
        <div>
            <span id="hour">{{displayHours}}</span>
            <span class="text">Hours</span>
        </div>
        <div>
            <span id="min">{{displayMinutes}}</span>
            <span class="text">Minutes</span>
        </div>
        <div>
            <span id="sec">{{displaySeconds}}</span>
            <span class="text">Seconds</span>
        </div>     
    </div>
    

  
</template>

<script>
export default {
    props:['year','month','date','hour','minutes','seconds','milliseconds'],
data:()=>({
    displayDays:0,
    displayHours:0,
    displayMinutes:0,
    displaySeconds:0,
    Loading:false
}),

computed:{
    secondsCal:()=>1000,
    minutesCal(){
        return this.secondsCal*60
        },
    hoursCal(){
        return this.minutesCal*60
        },
    daysCal(){
        return this.hoursCal*24
        },
        end(){
            return new Date(
                this.year,
                this.month,
                this.date,
                this.hour,
                this.minutes,
                this.seconds,
                this.milliseconds
            )
        }
},
mounted(){
    this.remainingTime()
},
methods:{
    formatNumber: num=>(num<10?'0'+num:num),
    remainingTime(){
        const timer=setInterval(()=>{
            const now=new Date();
            // const end=new Date(2022,9,24,10,10,10,10)
            const difference=this.end.getTime()-now.getTime();
            if(difference<0){
                clearInterval(timer)
                return
            }
            const days=Math.floor(difference/this.daysCal)
            // console.log(days);
            const hours=Math.floor((difference % this.daysCal)/this.hoursCal)
            // console.log(hours);
            const minutes=Math.floor((difference %this.hoursCal)/this.minutesCal)
            // console.log(min);
            const seconds=Math.floor((difference %this.minutesCal)/this.secondsCal)
            // console.log(sec);
            this.displayDays=this.formatNumber(days); 
            this.displayHours=this.formatNumber(hours); 
            this.displayMinutes=this.formatNumber(minutes); 
            this.displaySeconds=this.formatNumber(seconds); 
            this.Loading=true
        },1000)
    }
}
}
</script>

<style>
body{
    font-family: sans-serif;
    margin: 0;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    justify-content: center;
    background-size: cover;
    background-image: url("https://images.unsplash.com/photo-1444703686981-a3abbc4d4fe3?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80"); 
}
h2{
    text-transform: uppercase;
    letter-spacing: 4px;
    font-size: 14px;
    text-align: center;
    color: white;
}
.clock{
    display: flex;
}
.clock div{
    margin: 5px;
    position: relative;
}
.clock span{
    width: 100px;
    height: 80px;
    background-color: rgb(160, 83, 149);
    opacity: .8;
    color: white;
    justify-content: center;
    display: flex;
    align-items: center;
    font-size: 50px;
    text-shadow: 2px 2px 4px rgba(0, 	0, 0, 0.3);
}
.clock .text{
    height: 30px;
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 2px;
    background:rgb(33, 33, 80) ;
    opacity: 0.8;
}

.clock #ampm{
    bottom: 0;
    position: absolute;
    width: 60px;
    height: 30px;
    font-size: 20px;
    background: black;
}
</style>