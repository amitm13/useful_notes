<template>
    <div class="cantainer">
        <div class="h-100 w-5/12 mx-auto p-3 rounded bg-white font-semibold" v-if="loaded">
            <div class="grid grid-cols-4 gap-2">
                <div class="grid-cols-1">{{displayDay}} <br/>Day</div>
                <div class="grid-cols-2">{{displayHour}} <br/>Hours</div>
                <div class="grid-cols-3">{{displayMinute}} <br/>Min</div>
                <div class="grid-cols-4">{{displaySecond}} <br/>Sec</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Countdown',
    props:[
        'year',
        'month',
        'date',
        'hour',
        'minute',
        'seconds',
    ],
    data(){
        return{
            displayDay:0,
            displayHour:0,
            displayMinute:0,
            displaySecond:0,
            loaded:false
        }
    },
    computed:{
        _seconds: ()=>1000,
        _minutes(){
            return this._seconds*60;
        },
        _hours(){
            return this._minutes*60;
        },
        _days(){
            return this._hours*24;
        },
        userDate(){
            return new Date(this.year,this.month-1,this.date,this.hour,this.minute,this.seconds);
        }

    },
    mounted(){
        // start timer
        this.showTimer();
    },
    methods:{
        showTimer(){
            const countdown_timer = setInterval(() => {
                const now = new Date();
                const different = this.userDate.getTime() - now.getTime();
                if (different < 0) {
                    clearInterval(countdown_timer);
                    return;
                }
                
                const days = Math.floor(different / this._days);
                const hours = Math.floor((different % this._days) / this._hours);
                const minutes = Math.floor((different % this._hours) / this._minutes);
                const seconds = Math.floor((different % this._minutes) / this._seconds);

                this.displayDay = parseInt(days);
                this.displayHour = parseInt(hours);
                this.displayMinute = parseInt(minutes);
                this.displaySecond = parseInt(seconds);
                this.loaded = true;

            }, 1000);
        }
    }
}
</script>