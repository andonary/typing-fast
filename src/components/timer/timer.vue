<template>
    <div>
        {{ timer }}
    </div>
</template>

<script>
    export default {
        props: {
            userInput: {
                type: String,
                default: ''
            },
            finished: {
                type: Number,
                default: 0
            }
        },
        data() {
            return {
                firstInput: false,
                timer: '',
                dateCourante: 0,
                timerLaunch: undefined
            }
        },
        beforeDestroy() {
            this.timerLaunchClearInterval();
        },
        methods: {
            startTimer() {
                const delay = 100;
                this.timerLaunch = setInterval(() => {
                    let chrono = Math.round((new Date().getTime() - this.dateCourante) / 1000 * 10) / 10
                    if (Math.floor(chrono) === chrono) {
                        chrono = `${chrono}.0`
                    }
                    this.timer = `${chrono}`;
                }, delay);
            },
            stopTimer() {
                this.timerLaunchClearInterval();
                this.firstInput = false;
            },
            timerLaunchClearInterval() {
                clearInterval(this.timerLaunch);
            }
        },
        watch: {
            userInput: function() {
                if (!this.firstInput) {
                    this.firstInput = true;
                    this.dateCourante = new Date().getTime();
                    this.startTimer();
                }
            },
            finished: function() {
                if (this.finished > 0) {
                    this.stopTimer();
                }
            }
        }
    }
</script>
