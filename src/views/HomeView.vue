<script>
export default {
    data() {
        return {
            formPageCount: 0,
            totalFormPagesCount: 5,
        }
    },

    methods: {
        nextPage() {
            this.formPageCount++
        },

    },

    computed: {
        profressBarValue() {
            return Math.round(this.formPageCount * 100 / this.totalFormPagesCount)
        }
    }
}
</script>

<template>
    <v-container>
        <v-row no-gutters>
            <v-col cols="12" sm="12" md="10" lg="8">
                <p class="mt-10 mb-10 text-center">1 of 5</p>
                <div>
                    <v-progress-linear :model-value="profressBarValue" color="purple"></v-progress-linear>
                    <br>
                </div>
                <div v-if="formPageCount == 0">
                    <p>Upload document</p>
                </div>
                <div v-else-if="formPageCount == 1">
                    <p>Validate document data</p>
                </div>
                <div v-else-if="formPageCount == 2">
                    <p>Upload terminal photo</p>
                </div>
                <div v-else-if="formPageCount == 3">
                    <p>validate terminal photo</p>
                </div>
                <div v-else-if="formPageCount == 4">
                    <p>Upload shop images</p>
                </div>
                <div v-else-if="formPageCount > 4">
                    <p>Your appplication has been submitted!!!</p>
                </div>
                <v-btn variant="flat" rounded="pill" color="primary" class="mt-5" @click="nextPage()">
                    Next
                </v-btn>
            </v-col>
        </v-row>
    </v-container>
</template>
