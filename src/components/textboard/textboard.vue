<template>
    <div class="message">
        <div class="message-body">
            {{ getWord() }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            userInput: {
                type: String,
                default: ''
            }
        },
        data() {
            return {
                words: [
                    'héros',
                    'bonjour',
                    'bonsoir',
                    'salut',
                    'bernard',
                    'henry',
                    'julie',
                    'maman',
                    'maison',
                    'voiture',
                    'demain',
                    'soir',
                    'loutre',
                    'cheval',
                    'reine'
                ],
                currentIndex: 0,
                win: ''
            }
        },
        created() {
            this.shuffle(this.words);
        },
        methods: {
            getWord() {
                return this.words.slice(this.currentIndex, this.words.length + this.currentIndex).join(' ')
            },
            shuffle(words) {
                words.forEach((word, index) => {
                    const newIndex = Math.floor(Math.random() * (index + 1));
                    [words[index], words[newIndex]] = [words[newIndex], words[index]];
                });
                return words;
            },
            compareWord() {
                if (this.userInput.trim() === this.words[this.currentIndex]) {
                    this.$emit('win')
                    this.incrementWord()
                }
            },
            incrementWord() {
                this.currentIndex++
            }
        },
        watch: {
            userInput: function()  {
                this.compareWord();
            }
        }
    }
</script>
