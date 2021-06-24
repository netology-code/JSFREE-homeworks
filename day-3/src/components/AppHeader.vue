<template>
    <nav class="navbar navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Marvel</a>
            <form class="d-flex">
                <input
                        class="form-control me-2"
                        type="search"
                        placeholder="Поиск..."
                        aria-label="Search"
                        v-model.trim="search"
                        @keypress.enter.prevent
                        @input="changeSearch(search)"
                >
                <button
                        class="btn btn-outline-light"
                        type="reset"
                        @click="()=>{search=''; changeSearch(search)}"
                >все
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
    export default {
        name: "AppHeader",
        props: ['changeSearch'],
        data() {
            return {
                search: '',
            }
        },
    }
</script>

<style scoped>

</style>
