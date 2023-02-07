<script>
import axios from "axios";
axios.defaults.baseURL =
    "https://1ydvd2q6ka.execute-api.us-east-1.amazonaws.com/";

export default {
    data() {
        return {
            formPageCount: 1,
            totalFormPagesCount: 5,
            formValid: false,

            valid: false,
            firstname: "",
            lastname: "",
            nameRules: [
                (value) => {
                    if (value) return true;

                    return "Name is requred.";
                },
                (value) => {
                    if (value?.length <= 20) return true;

                    return "Name must be less than 20 characters.";
                },
            ],
            email: "",
            emailRules: [
                (value) => {
                    if (value) return true;

                    return "E-mail is requred.";
                },
                (value) => {
                    if (/.+@.+\..+/.test(value)) return true;

                    return "E-mail must be valid.";
                },
            ],

            identityNumber: "",
            identityRules: [
                (value) => {
                    if (value) return true;

                    return "Identity Number is requred.";
                },
                (value) => {
                    if (value?.length <= 20) return true;

                    return "Name must be less than 10 characters.";
                },
            ],

            genders: ["Male", "Female", "Other"],

            idImage: null,
            terminalImage: null,
            inspectionImages: null,
            imageRules: [
                (value) => {
                    if (value) return true;

                    return "Image is requred.";
                },
                (value) => {
                    return (
                        !value ||
                        !value.length ||
                        value[0].size < 2000000 ||
                        "Image size should be less than 2 MB!"
                    );
                },
            ],

            buttonLoading: false,
            errorMessage: "",
            snackbar: false,
            snackbarTimeout: 3000,
        };
    },

    methods: {
        processNext() {
            this.buttonLoading = true;

            if (this.formPageCount == 1) {
                this.uploadIDImage();
            } else if (this.formPageCount == 2) {
                console.log("2");
            } else if (this.formPageCount == 3) {
                console.log("3");
            } else if (this.formPageCount == 4) {
                console.log("4");
            } else if (this.formPageCount == 5) {
                console.log("5");
            } else if (this.formPageCount == 6) {
                console.log("6");
            }
        },

        validateInput() {
            let vm = this;
            let isValid = this.$refs.form.validate().then(function (formSubmission) {
                if (formSubmission.valid) {
                    vm.processNext();
                }
            });
        },

        nextPage() {
            this.formPageCount++;
        },

        // getFileInBase64(file) {
        //     return new Promise((resolve, reject) => {
        //         const reader = new FileReader();
        //         reader.readAsDataURL(file);
        //         reader.onload = () => resolve(reader.result);
        //         reader.onerror = (error) => reject(error);
        //     });
        // },

        async uploadIDImage() {
            let formData = new FormData();

            // for (let image of this.idImage) {
            //     let result = await this.getFileInBase64(image).then(
            //         (res) => {
            //             formData.append("id-doc", String(res));
            //         },
            //         (failure) => {
            //             console.error(failure);
            //         }
            //     );
            // }

            for (let image of this.idImage) {
                formData.append("id-doc", image);
            }

            const response = await axios
                .post("v1/uploadcontent/", formData, {
                    headers: {
                        'Content-Type': 'multipart/form-data',
                    },
                })
                .then((response) => {
                    console.log(response.code);
                    if (response.code == 200) {
                        this.nextPage();
                    } else {
                        this.errorMessage = "Oops! Failed to upload image.";
                        this.snackbar = true;
                    }
                })
                .catch((error) => {
                    this.errorMessage = "Oops! Something went wrong.";
                    this.snackbar = true;
                });

            this.buttonLoading = false;
        },
    },

    computed: {
        profressBarValue() {
            return Math.round((this.formPageCount * 100) / this.totalFormPagesCount);
        },
    },
};
</script>

<template>
    <v-container>
        <v-row justify="center" no-gutters>
            <v-col cols="12" sm="12" md="10" lg="8">
                <p v-if="formPageCount < 6" class="mt-10 mb-10 text-center"
                    style="font-weight: 500; font-size: large; color: #636b30">
                    {{ formPageCount }} of {{ totalFormPagesCount }}
                </p>
                <div v-if="formPageCount < 6" class="mb-5">
                    <v-progress-linear :model-value="profressBarValue" color="#97a93d" :height="5"></v-progress-linear>
                    <br />
                </div>
                <div v-if="formPageCount == 1">
                    <p class="text-center mb-5" style="font-size: 30px; font-weight: 600; color: #636b30">
                        Identification
                    </p>
                    <br />
                    <p class="mb-5 mt-5 text-center" style="padding: 10px; font-size: 19px">
                        Upload an image of your asylum document. Please ensure the image of
                        the document is well lit and all the contents are clearly visible.
                    </p>
                    <v-form v-model="formValid" ref="form">
                        <v-file-input v-model="idImage" :rules="imageRules" accept="image/png, image/jpeg, image/bmp"
                            prepend-icon="mdi-camera" label="Asylum Document" v-on:keyup.enter="validateInput"
                            show-size></v-file-input>
                        <div class="d-flex justify-center align-baseline" style="padding-right: 5px">
                            <v-spacer></v-spacer>
                            <v-btn variant="flat" append-icon="mdi-arrow-right" rounded="pill" color="#97a93d"
                                class="mt-5" size="large" @click="validateInput()" :loading="buttonLoading">
                                Next
                            </v-btn>
                        </div>
                    </v-form>

                    <br /><br />
                </div>
                <div v-else-if="formPageCount == 2">
                    <p class="text-center mb-5" style="font-size: 30px; font-weight: 600; color: #636b30">
                        Identification
                    </p>
                    <br />
                    <p style="padding: 10px">Confirm document data:</p>
                    <v-form v-model="formValid" ref="form">
                        <v-container>
                            <v-row justify="center">
                                <v-col cols="12" md="6">
                                    <v-text-field v-model="firstname" :rules="nameRules" :counter="20"
                                        label="First name" variant="outlined" required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="6">
                                    <v-text-field v-model="lastname" :rules="nameRules" :counter="20" label="Last name"
                                        variant="outlined" required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="6">
                                    <v-text-field v-model="identityNumber" :rules="identityRules" :counter="13"
                                        label="Identity Number" variant="outlined" required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="6">
                                    <v-select :items="genders" label="Gender" variant="outlined" required></v-select>
                                </v-col>
                            </v-row>
                            <div class="d-flex justify-center align-baseline" style="padding-right: 5px">
                                <v-spacer></v-spacer>
                                <v-btn variant="flat" append-icon="mdi-arrow-right" rounded="pill" color="#97a93d"
                                    class="mt-5" size="large" @click="validateInput()" :loading="buttonLoading">
                                    Next
                                </v-btn>
                            </div>
                        </v-container>
                    </v-form>
                </div>
                <div v-else-if="formPageCount == 3">
                    <p class="text-center mb-5" style="font-size: 30px; font-weight: 600; color: #636b30">
                        Merchant Terminal
                    </p>
                    <br />
                    <p>Upload terminal photo</p>
                </div>
                <div v-else-if="formPageCount == 4">
                    <p class="text-center mb-5" style="font-size: 30px; font-weight: 600; color: #636b30">
                        Merchant Terminal
                    </p>
                    <br />
                    <p class="mb-3" style="padding: 10px">
                        Confirm terminal information:
                    </p>
                </div>
                <div v-else-if="formPageCount == 5">
                    <p class="text-center mb-5" style="font-size: 30px; font-weight: 600; color: #636b30">
                        Site Inspection
                    </p>
                    <br />
                    <p>Upload shop images</p>
                </div>
                <div v-else-if="formPageCount > 5" class="text-center">
                    <br /><br /><br /><br />
                    <v-icon icon="mdi mdi-checkbox-marked-circle-outline" size="200" class="mt-5 mb-5"
                        color="#97a93d"></v-icon>
                    <p class="mt-5" style="font-size: x-large">
                        Your application has been submitted!
                    </p>
                </div>

                <v-snackbar v-model="snackbar" :timeout="snackbarTimeout" color="#FF312E">
                    {{ errorMessage }}

                    <template v-slot:actions>
                        <v-btn color="white" variant="text" @click="snackbar = false" style="background: grey">
                            Close
                        </v-btn>
                    </template>
                </v-snackbar>
            </v-col>
        </v-row>
    </v-container>
</template>
