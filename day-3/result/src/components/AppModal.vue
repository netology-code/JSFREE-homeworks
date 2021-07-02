<template>
    <!-- Modal -->
    <div v-if="character"
         class="modal fade"
         id="exampleModal"
         tabindex="-1"
         aria-labelledby="exampleModalLabel"
         aria-hidden="true"
    >
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">
                        {{character.name}}
                    </h5>
                    <button
                            type="button"
                            class="btn-close"
                            data-bs-dismiss="modal"
                            aria-label="Close">
                    </button>
                </div>
                <div class="modal-body">
                    <img
                            style="max-width: 100%;"
                            :src="character.thumbnail"
                            :alt="character.name"
                    >
                    <div>
                        <p class="text-muted">{{character.modified}}</p>

                        <h5>Описание:</h5>
                        <p>{{character.description}}</p>

                        <h5>Комиксы:</h5>
                        <ul>
                            <li v-for="(elComics, idx) in character.comics"
                                :key="idx"
                            >
                                {{elComics.name}}
                            </li>
                        </ul>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary  btn-sm" data-bs-dismiss="modal">
                            Закрыть
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "AppModal",
        props: ['character'],
    }
</script>

<style scoped>

</style>
