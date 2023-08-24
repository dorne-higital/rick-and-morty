<template>
    <div 
        class="card-container"
        @click="openModal"
    >
        <img :src="character.image" :alt="character.name" />

        <div class="character-info">
            <h3>{{ character.name }}</h3>

            <p>Gender: {{ character.gender }}</p>
        </div>

        
  </div>
</template>
  
<script>
    export default {
        props: ["character"],
        methods: {
            openModal() {
                this.$emit('show-modal', this.character);
                console.log('text');
            }
        },
        computed: {
            cardStyle() {
                return {
                    // backgroundImage: `url(${this.character.image})`
                };
            }
        },
    };
</script>

<style scoped lang="scss">
    .card-container {
        align-items: center;
        background: #afd5df;
        border-radius: 0.5rem;
        display: flex;
        flex-direction: row;
        gap: 1rem;
        height: 100%;
        outline: 1px solid #000;
        padding: .5rem;
        text-align: left;
        transition: 0.3s;

        @media only screen and (min-width: 1024px) {
            padding: 1rem;
            width: calc((100% / 4) - 0.5rem)
        }

        @media only screen and (min-width: 768px) {
            flex-direction: column;
            height: fit-content;
            width: calc(40% - 2rem);
        }

        &:hover {
            background: #53c781;
            cursor: pointer;
            transition: 0.3s;
        }

        .character-info {
            padding: 0 1rem;

            h3 {
                font-weight: 500;
            }
        }

        img {
            border-radius: 0.5rem;
            box-shadow: 0 0 5px 1px #262d3b;
            height: 6rem;
            outline: 1px solid #000;
            width: 6rem;

            @media only screen and (min-width: 1280px) {
                height: 15rem;
                width: 15rem;
            }

            @media only screen and (min-width: 768px) {
                height: auto;
                width: 100%;
            }
        }
    }
</style>
  