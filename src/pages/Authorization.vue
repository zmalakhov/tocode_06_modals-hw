<template>
    <div class="wrapper-content wrapper-content--fixed">
        <section>
            <div class="container">
                <h1>Authorization page</h1>

                <!-- modalLogin -->
                <button class="btn btnPrimary" @click="showModalLogin = !showModalLogin">Show modal Login</button>
                <modalLogin v-show="showModalLogin"
                        @close="showModalLogin=false"
                        @changeFormLoginRegistr="changeFormLoginRegistr"
                >
                </modalLogin>

                <!-- modalRegistration -->
                <button class="btn btnPrimary" @click="showModalRegistration = !showModalRegistration">Show modal Registration</button>
                <modalRegistration v-show="showModalRegistration"
                                   @close="showModalRegistration=false"
                                   @changeFormLoginRegistr="changeFormLoginRegistr"
                >
                </modalRegistration>

            </div>
        </section>
    </div>
</template>

<script>

    import modals from '@/components/UI/Modal.vue'
    import modalLogin from '@/components/authorization/ModalLogin'
    import modalRegistration from '@/components/authorization/ModalRegistration'

    export default {
        components: {modals, modalLogin, modalRegistration},
        data(){
            return {
                showModalLogin: false,
                showModalRegistration: false,
            }

        },
        methods:{
            changeFormLoginRegistr(){
                this.showModalLogin = !this.showModalLogin
                this.showModalRegistration = !this.showModalRegistration
            }
        }
    }
</script>

<style lang="scss" scoped>
    h1{
        margin-bottom: 30px;
    }
</style>