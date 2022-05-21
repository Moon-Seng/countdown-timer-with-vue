<template>
    <div>
        <section v-if="!experied" class="mt-4 text-4xl mb-8">New Year Countdown</section>
        <section v-else class="mt-4 text-4xl mb-8">Happy New Year</section>

        <section v-if="load" class="flex text-8xl align-middle justify-center mr-4">
            <div class="days flex justify-center relative pb-4 flex-col ">
                {{displayDays}}
                <div class="text-sm absolute bottom-0 inset-x-0">days</div>
            </div>
            <div class="leading-snug mx-8">:</div>


            <div class="days flex justify-center relative pb-4 flex-col ">
                {{displayHours}}
                <div class="text-sm absolute bottom-0 inset-x-0">hours</div>
            </div>
            <div class="leading-snug mx-8">:</div>


            <div class="days flex justify-center relative pb-4 flex-col ">
                {{displayMinutes}}
                <div class="text-sm absolute bottom-0 inset-x-0">minutes</div>
            </div>
            <div class="leading-snug mx-8">:</div>

            <div class="days flex justify-center relative pb-4 flex-col ">
                {{displaySeconds}}
                <div class="text-sm absolute bottom-0 inset-x-0">seconds</div>
            </div>

        </section>

    </div>
</template>

<script>
    export default {
        name : 'countComponent',
        props: ['propsDays', 'propsYear' , 'propsMonths'],
        data(){
            return{
                displayDays : 0,
                displayHours : 0,
                displayMinutes : 0,
                displaySeconds : 0,
                load : false,
                experied : false ,
                end(){
                    return new Date(this.propsYear, this.propsMonths , this.propsDays);
                }
            }
        },
        mounted(){
            this.showRemaining();
        },
        methods: {
            showRemaining(){
                const timer = setInterval(()=>{
                    const now = new Date();
                    // const end = new Date(2023,0,1);

                    const distance = this.end().getTime() - now.getTime()

                    if(distance < 0){
                        clearInterval(timer);
                        this.load = true;
                        this.experied = true
                        return
                    }

                    let miliseconds = Math.floor(distance/1000);

                    let seconds = Math.floor(miliseconds) % 60;
                    let minutes = Math.floor(miliseconds / 60) % 60;
                    let hours = Math.floor(miliseconds / 3600) %24;
                    let days = Math.floor(miliseconds / 3600 / 24)
                    // console.log(days , hours , minutes , seconds ,miliseconds );

                    this.displayDays = this.formatNum(days);
                    this.displayHours = this.formatNum(hours);
                    this.displayMinutes = this.formatNum(minutes);
                    this.displaySeconds = this.formatNum(seconds);
                    this.load = true
                },1000)

                timer
            },
            formatNum(num){
                return num < 10 ? "0"+ num : num; 
            }
        }

    }
</script>

<style scoped>

</style>