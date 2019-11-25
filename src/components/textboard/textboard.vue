<template>
    <div class="message">
        <div class="message-body" v-html="displayWords()">
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
            displayWords() {
                const words = this.getWords();
                words[0] = `<strong>${words[0]}</strong>`;
                return words.join(' ')
            },
            getWords() {
                const maxLength = this.words.length;
                const index = this.currentIndex % maxLength;
                if (this.currentIndex > 0 && index === 0) {
                    this.$emit('finished')
                    this.currentIndex = 0;
                    this.shuffle(this.words);
                }
                return this.words.slice(index, maxLength);
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

