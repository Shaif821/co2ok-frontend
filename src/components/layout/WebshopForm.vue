<template>
    <div class="uk-section section-1">
        <div class="uk-container form__section uk-container-width">
            <div class="uk-flex uk-flex-wrap uk-flex-wrap-around col-1" uk-grid>
                <div class="uk-width-1-2 to-left">
                    <div class="uk-card uk-card-body section-1__col-1 final__section">
                        <h2 class="main-title--large">{{content === 1 ? locale['title1'] : locale['title2']}}</h2>
                        <p class="main-text--large">
                            {{content === 1 ? locale['subtitle1'] : locale['subtitle2']}}
                        </p>
                    </div>
                </div>

                <div class="uk-width-1-2 to-right">
                    <div class="uk-card login__form-container col-2-card uk-card-default uk-card-body">
                        <form class="login__form">
                            <div class="login__group">
                                <label class="login__group">
                                    {{locale['input1_label']}}
                                    <input v-model="name"
                                           class="login__group-input" type="email"
                                           :placeholder="locale['input1_field']">
                                </label>

                                <label class="login__group">
                                    <span>{{locale['input2_label']}}<span class="asterik">*</span></span>
                                    <input v-model="email"
                                           class="login__group-input" type="email"
                                           :placeholder="locale['input2_field']">
                                </label>

                                <label class="login__group">
                                    {{locale['input3_label']}}
                                    <input v-model="phone"
                                           class="login__group-input" type="email"
                                           :placeholder="locale['input3_field']">
                                </label>

                                <label class="login__group">
                                    {{locale['input4_label']}}
                                    <input v-model="platform"
                                           class="login__group-input" type="email"
                                           :placeholder="locale['input4_field']">
                                </label>
                            </div>

                            <div style="width: 100%; text-align: left;" class="login__buttons">
                                <a class="button button-empty btn-large" @click="emptyForm()"> {{locale['empty']}}</a>
                                <a class="button btn-large" @click="sendForm()"> {{locale['send']}}</a>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    const Modal = () => import('@/components/modals/Modal')
    import language from '../../lang/lang_webshopform'

    export default {
        name: "WebshopForm",
        props: {
            content: Number
        },
        components: {
            Modal
        },


        data() {
            return {
                locale: language,
                name: '',
                email: '',
                phone: '',
                platform: '',
            }
        },

        mounted() {
            this.checkLanguage()

        },

        methods: {
            checkLanguage(lang) {
                if(lang === 'en'){
                    this.locale = language.lang_en_webshopform
                } else {
                    if (this.currentLanguage === 'en') {
                        this.locale = language.lang_en_webshopform
                    } else {
                        this.locale = language.lang_nl_webshopform
                    }
                }
            },

            emptyForm() {
                this.name = ''
                this.email = ''
                this.phone = ''
                this.platform = ''
            },

            //Deze functie kan je gebruiken wanneer de data daadwerkelijk verstuurd zijn
            //Voor de vormgeving heb ik de modal al aangemaakt
            //Voor de form is alleen de email verplicht
            //De else statemant is bedoeld als de email form leeg is
            sendForm() {
                if(this.email !== ''){
                    let message = {
                        title: this.locale['success'],
                        text: this.locale['success_message']
                    }
                    this.$store.commit('modalStatus', {message})
                }
                else {
                    let message = {
                        title: this.locale['error'],
                        text: this.locale['error_message']
                    }
                    this.$store.commit('modalStatus', {message})
                }
            }
        },

        computed: {
            currentLanguage() {
                return this.$store.state.language
            }
        },

        watch: {
            currentLanguage(value) {
                this.checkLanguage(value)
            }
        }
    }
</script>

<style scoped lang="scss">
    @import '../../styles/layout/main';
    @import '../../styles/webshops/webshop__form';
</style>