<template>
    <div class="containr">
        <div class="search-results">
            <!-- <h2>Search Results</h2> -->

            <div class="cards-container">
                <CharacterCard
                    v-for="character in displayedCharacters"
                    :key="character.id"
                    :character="character"
                    @show-modal="showModal"
                />
            </div>

            <Modal 
                v-if="modalVisible" 
                :character="selectedCharacter" 
                @close-modal="closeModal" 
            />
        </div>

    </div>
</template>
  
<script>
import CharacterCard from './CharacterCard.vue';
import Modal from './Modal.vue';

export default {
    props: ['characters', 'searchQuery'],
    components: {
        CharacterCard,
        Modal
    },
    data() {
        return {
            page: 1,
            pages: 1,
            charactersPerPage: 4,
            modalVisible: false,
            selectedCharacter: {}
        };
    },
    computed: {
        filteredCharacters() {
            if (this.searchQuery) {
            return this.characters.filter(character =>
                character.name.toLowerCase().includes(this.searchQuery.toLowerCase())
            );
            } else {
                return this.characters;
            }
        },
        displayedCharacters() {
            const startIndex = (this.page - 1) * this.charactersPerPage;
            const endIndex = startIndex + this.charactersPerPage;
            return this.filteredCharacters.slice(startIndex, endIndex);
        },
        changePage(page) {
            this.page = page <= 0 || page > this.pages ? this.page : page;
            this.fetch();
        },
    },
    methods: {
        changePage(page) {
            this.page = page <= 0 || page > this.pages ? this.page : page;
            this.fetch();
        },
        showModal(character) {
            this.selectedCharacter = character;
            this.modalVisible = true;
        },
        closeModal() {
            this.modalVisible = false;
            this.selectedCharacter = {};
        }
    }
};
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

h2 {
    margin-bottom: 1.5rem;
}
.search-results {
    display: flex;
    flex-direction: column;
    height: 65vh;
    gap: 1rem;
    overflow: hidden;
    padding: 1rem;
    width: calc(100vw);

    @media only screen and (min-width: 1280px) {
        height: 50vh;
        padding: 2rem 0 2rem 2rem;
        width: 70vw;
    }

    .cards-container {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        width: 100%;

        @media only screen and (min-width: 1280px) {
            gap: 0.5rem;
            flex-wrap: nowrap;
        }

        @media only screen and (min-width: 768px) {
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: center;
        }
    }
}
</style>
  