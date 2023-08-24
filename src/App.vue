<template>
    <div class="main-container">
        <Search @search="searchData" />
        <SearchResults
            :characters="characters"
            :searchQuery="search"
        />

        <Modal 
            v-if="modalVisible" 
            :character="selectedCharacter" 
            @close-modal="closeModal" 
        />

        <div class="pagination">
            <button @click="changePage(page - 1)" :disabled="page === 1">Previous</button>
                <span>{{ page }} / {{ pages }}</span>
            <button @click="changePage(page + 1)" :disabled="page === pages">Next</button>
        </div>
    </div>
</template>
  
<script>
    import axios from "axios";
    import Search from './components/Search.vue';
    import SearchResults from './components/SearchResults.vue';
  
  export default {
    name: 'App',
    components: {
      Search,
      SearchResults,
    },
    data: function() {
      return {
        characters: [],
        page: 1,
        pages: 1,
        search: "",
        currentCharacter: {}
      };
    },
    created() {
      this.fetch();
    },
    methods: {
      fetch() {
        const params = {
          page: this.page,
          name: this.search
        };
  
        let url = "https://rickandmortyapi.com/api/character";
        let result = axios
            .get(url, { params })
            .then(res => {
              this.characters = res.data.results;
              this.pages = res.data.info.pages;
              console.log(this.characters);
            })
            .catch(console.log);
      },
      changePage(page) {
        this.page = page <= 0 || page > this.pages ? this.page : page;
        this.fetch();
      },
      searchData(query) {
        this.search = query;
        this.page = 1; // Reset page to 1 when performing a new search
        this.fetch();
      },
      async fetchOne(id) {
        let result = await axios.get(
            `https://rickandmortyapi.com/api/character/${id}/`
        );
        this.currentCharacter = result.data;
        this.modal = true;
      }
    }
  };
</script>
  

<style lang="scss">

*,
*::before,
*::after {
    box-sizing: border-box;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    scroll-behavior: smooth;
}

body,
h1,
h2,
h3,
h4,
p {
    margin: 0;
}

ul[role='list'],
ol[role='list'] {
    list-style: none;
}

body {
    background: #ebebee;
    color: #3a4767;
    width: 100%;
}

.main-container {
    background-image: url('@/assets/rick-bg.png');
    box-shadow: 0 0 8px 1px #262d3b;
    height: 100vh;
    margin: auto;
    outline: 1px solid #ebebee;
    text-align: center;
    width: 100vw;

    @media only screen and (min-width: 1280px) {
        border-radius: 0.5rem;
        height: calc(100vh - 2rem);
        width: calc(100vw - 2rem);
    }

    .pagination {
        height: 10vh;
        width: 100vw;

        @media only screen and (min-width: 1280px) {
            height: 15vh;
            width: 70vw;
        }

        button {
            background: #b4eefd;
            border: 1px solid #b4eefd;
            border-radius: 0.5rem;
            cursor: pointer;
            padding: 0.5rem;
            width: 7rem;

            &:disabled {
                background: #818384;
                border: 1px solid #818384;
                cursor: auto;

                &:hover {
                    border: 1px solid #818384;
                }
            }

            &:hover {
                border: 1px solid #6adbf7;
            }
        }

        span {
            color: #ebebee;
            font-size: 0.9rem;
            padding: 1rem;
        }
    }
}
</style>
