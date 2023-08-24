<template>
    <div class="modal">
        <div class="modal-content">
            <button 
                class="close-button" 
                @click="closeModal"
            >
                &times;
            </button>

            <img 
                :src="character.image" 
                :alt="character.name" 
            />

            <h1>{{ character.name }}</h1>

            <h3>Key details</h3>

            <div class="content">
                <span class="item">
                    <label>Gender: </label>
                    <p>{{ character.gender }}</p>
                </span>

                <span class="item">
                    <label>Status: </label>
                    <p>{{ character.status }}</p>
                </span>

                <span class="item">
                    <label>Species: </label>
                    <p>{{ character.species }}</p>
                </span>

                <span class="item">
                    <label>Type: </label>
                    <p>{{ character.type || 'n/a' }}</p>
                </span>
            </div>

            <h3>Location</h3>

            <div class="content">
                <span class="item">
                    <label>Origin: </label>
                    <p>{{ character.origin.name }}</p>
                </span>

                <span class="item">
                    <label>Current: </label>
                    <p>{{ character.location.name }}</p>
                </span>
            </div>

            <h3>Episodes</h3>

            <div class="content">
                <span class="item">
                    <label># Episodes in: </label>
                    <p>{{ character.episode.length }}</p>
                </span>
            </div>
        </div>

        <div class="modal-overlay" @click="closeModal"></div>
    </div>
</template>
  
<script>
export default {
    props: ['character'],
    methods: {
        closeModal() {
            this.$emit('close-modal');
        }
    }
};
</script>
  
<style scoped lang="scss">

.modal {
    align-items: center;
    display: flex;
    height: 100%;
    justify-content: center;
    left: 0;
    position: fixed;
    top: 0;
    width: 100%;

    .modal-overlay {
        background-color: rgba(0, 0, 0, 0.6);
        height: 100%;
        left: 0;
        position: absolute;
        top: 0;
        width: 100%;
    }

    .modal-content {
        background-color: #afd5df;
        border-radius: 8px;
        color: #111111;
        height: calc(100vh - 2rem);
        overflow: auto;
        padding: 20px;
        position: absolute;
        right: 1rem;
        text-align: center;
        width: calc(100vw - 2rem);
        z-index: 99;

        @media only screen and (min-width: 1280px) {
            height: calc(100vh - 2rem);
            width: 30vw;
        }

        h1 {
            font-weight: 100;
            margin-bottom: 1rem;
        }

        h3 {
            font-weight: 300;
            margin: 1rem;
        }

        img {
            border-radius: 0.5rem;
            box-shadow: 0 0 5px 1px #262d3b;
            outline: 1px solid #000;
            width: 70%;
        }

        .close-button {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 3rem;
            position: absolute;
            right: 0.5rem;
            top: 0.5rem;

            @media only screen and (min-width: 1280px) {
                display: none;
            }
        }

        .content {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            justify-content: center;

            .item {
                background: #ffffff5a;
                border-radius: 0.5rem;
                box-shadow: 0 0 4px 1px #262d3b;
                outline: 1px solid #fff;
                padding: 0.5rem;
                transition: 0.3s;
                width: 8rem;

                &:hover {
                    background: #ffffff82;
                    transition: 0.3s;
                }

                @media only screen and (min-width: 1280px) {
                    width: 10rem;
                }

                label {
                    font-size: 0.7rem;
                }

                p {
                    font-size: 0.9rem;
                    font-weight: 600;
                }
            }
        }
    }
}

</style>
