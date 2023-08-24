<template>
    <div class="search-container">
        <h1>Rick<span>&</span>Morty</h1>

        <h3>Character finder</h3>

        <input 
            v-model="searchQuery" 
            @input="handleInput" 
            placeholder="Search a character" 
        />
    </div>
</template>
  
<script>
    export default {
        name: 'Search',
        data() {
            return {
                searchQuery: ''
            };
        },
        methods: {
            handleInput() {
                this.$emit('search', this.searchQuery);
            }
        }
    }
</script>
  
<style scoped lang="scss">
    .search-container {
        align-content: center;
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 25vh;
        width: 100%;

        @media only screen and (min-width: 1280px) {
            height: 35vh;
            margin: 1rem;
            padding: 1rem;
            width: 70vw
        }

        @media only screen and (min-width: 768px) {
            height: 30vh;
        }

        h1 {
            color: #ebebee;
            font-weight: 900;
            font-size: 3rem;

            @media only screen and (min-width: 1280px) {
                font-size: 6rem;
            }

            @media only screen and (min-width: 768px) {
                font-size: 4.5rem;
            }

            span {
                color: #404a5e;
            }
        }

        h3 {
            color: #ebebee7b;
            font-size: 1.5rem;
            font-weight: 100;
            margin-top: -1rem;
            margin-bottom: 1rem;

            @media only screen and (min-width: 1280px) {
                font-size: 2rem;
                margin-top: -1.5rem;
            }
        }

        input {
            background: #ebebeec7;
            border-radius: 0.5rem;
            box-shadow: 0 4px 30px #0000001a;
            backdrop-filter: blur(5px);
            -webkit-backdrop-filter: blur(5px);
            border: 1px solid #ffffff69;
            font-size: 1.2rem;
            height: 3.5rem;
            margin: 0 auto;
            padding: 1rem 0.5rem;
            width: 90%;

            @media only screen and (min-width: 1280px) {
                width: 100%;
            }

            &:focus {
                background: #ebebee;
                outline: none;
            }
        }
    }
</style>
  