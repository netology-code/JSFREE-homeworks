<template>
    <div id="app">
        <app-header :changeSearch="changeSearch"/>

        <div class="container">
            <h1 class="pt-3 pb-3">Персонажи Marvel</h1>

            <app-modal :character="character"/>
            <spinner v-if="loading"/>
            <div v-else class="row">
                <h5 v-if="!searchCharacters.length">Ничего не найдено</h5>
                <div v-else
                     v-for="(el, idx) in searchCharacters"
                     :key="el.id"
                     class="card mb-3 col-sm-12 col-md-6 col-lg-4">
                    <div class="row g-0">
                        <div class="col-4">
                            <img
                                    style="max-width: 100%;"
                                    :src="el.thumbnail"
                                    :alt="el.name"
                            >
                        </div>
                        <div class="col-8">
                            <div class="card-body">
                                <h5 class="card-title">{{el.name}}</h5>

                                <button
                                        type="button"
                                        class="btn btn-secondary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#exampleModal"
                                        @click="characterIndex = idx"
                                >
                                    Подробнее
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
    import Spinner from "./components/Spinner";
    import AppModal from "./components/AppModal";
    import AppHeader from "./components/AppHeader";

    export default {
        name: 'App',
        components: {
            AppHeader,
            AppModal,
            Spinner,
        },
        data() {
            return {
                loading: false,
                characters: [],
                characterIndex: 0,
                search: '',
            }
        },
        methods: {
            fetchCharacters: function () {
                return fetch(`https://netology-api-marvel.herokuapp.com/characters`)
                    .then(response => response.json())
                    .then(json => this.characters = json)
            },
            changeSearch: function (value) {
                this.search = value
            }
        },
        computed: {
            character: function () {
                return this.searchCharacters[this.characterIndex] || null
            },
            searchCharacters: function () {
                const {characters, search} = this;
                return characters.filter((character) => {
                    return character.name.toLowerCase().indexOf(search.toLowerCase()) !== -1
                })
            },
        },
        async mounted() {
            this.loading = true
            await this.fetchCharacters()
            this.loading = false
        }
    }
</script>

<style>

</style>
