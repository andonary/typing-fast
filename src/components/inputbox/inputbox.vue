<template>
    <div class="field">
        <div class="control">
            <input class="input is-large" autofocus type="text" placeholder="" v-model="inputValue" v-on:input="$emit('userInput', $event.target.value)">
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            deleteInput: {
                type: Number,
                default: 0
            }
        },
        data() {
            return {
                inputValue: '',
            }
        },
        methods: {
            clear() {
                this.test = 'ok';
                if (this.deleteInput !== 0) {
                    this.inputValue = ''
                }
            }
        },
        watch: {
            deleteInput: function() {
                this.clear();
            }
        }
    }
</script>
