<template>
    <modal
            title="Form Login"
            @close="close"
    >
        <!-- body -->
        <div slot="body">
            <form @submit.prevent="onSubmit">
                <!--email-->
                <div class="form-item" :class="{ errorInput: $v.email.$error }">
                    <label>Email:</label>
                    <p class="errorText" v-if="!$v.email.required">Field is required!</p>
                    <p class="errorText" v-if="!$v.email.email">Email is not correct!</p>
                    <input
                            v-model="email"
                            :class="{ error: $v.email.$error }"
                            @change="$v.email.$touch()"
                    >
                </div>
                <!--password-->
                <div class="form-item" :class="{ errorInput: $v.password.$error }">
                    <label>Password:</label>
                    <p class="errorText" v-if="!$v.password.required">Field is required!</p>
                    <p class="errorText" v-if="!$v.password.minLength">Name must have at least {{
                        $v.password.$params.minLength.min }} !</p>
                    <input
                            v-model="password"
                            :class="{ error: $v.password.$error }"
                            @change="$v.password.$touch()"
                    >
                </div>
                <!--button-->
                <button class="btn btnPrimary">Submit</button>
            </form>
            <br>
            <span class="link" @click="changeFormLoginRegistr">I need an account</span>
        </div>
    </modal>
</template>

<script>
    import {required, minLength, email, sameAs} from 'vuelidate/lib/validators'
    import modal from '@/components/UI/Modal.vue'

    export default {
        components: {modal},
        data() {
            return {
                email: '',
                password: '',
            }
        },
        validations: {
            email: {
                required,
                email
            },
            password: {
                required,
                minLength: minLength(7)
            },
        },
        methods: {
            onSubmit() {
                this.$v.$touch()
                if (!this.$v.$invalid) {
                    const user = {
                        email: this.email,
                        password: this.password,
                    }
                    console.log(user);

                    // DONE!
                    this.close()
                }
            },
            close() {
                // close
                this.$emit('close')

                // reset
                this.resetData()
            },
            resetData() {
                this.email = ''
                this.password = ''
                this.$v.$reset()
            },
            changeFormLoginRegistr(){
                this.resetData()
                this.$emit('changeFormLoginRegistr')
            }
        }
    }
</script>

<style lang="scss">
    .form-item .errorText {
        display: none;
        margin-bottom: 8px;
        font-size: 13.4px;
        color: #de4040;
    }

    .form-item {
        &.errorInput .errorText {
            display: block;
        }
    }

    input.error {
        border-color: #de4040;
    }
</style>