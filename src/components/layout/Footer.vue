<template>
    <footer id="footer" style="text-align: left;">
        <div class="uk-container footer-container">
            <div uk-grid>
                <div class="uk-width-1-3@m footer-column">
                    <h2>Contact</h2>
                    <ul>
                        <li>Lange Viestraat 2</li>
                        <li>3511 BK, Utrecht (De Planeet)</li>
                        <li>+31 (0) 6 397 65 259</li>
                        <li>info@co2ok.eco</li>
                        <li>© 2019 CO₂ok.</li>
                        <li>{{locale['kvk']}} 69752753</li>
                    </ul>
                </div>
                <div class="uk-width-1-3@m footer-column">
                    <h2>Sitemap</h2>
                    <ul>
                        <li>
                            <router-link to="/">{{locale['link1']}}</router-link>
                        </li>
                        <li>
                            <router-link to="/about">{{locale['link2']}}</router-link>
                        </li>
                        <li>
                            <router-link to="/webshops">{{locale['link3']}}</router-link>
                        </li>
                        <li>
                            <router-link to="/compensation">{{locale['link4']}}</router-link>
                        </li>
                        <li>
                            <ul>
                                <li>
                                    <router-link to="/webshops/retailers">{{locale['link5']}}</router-link>
                                </li>
                                <li>
                                    <router-link to="webshops/cause-marketing">{{locale['link6']}}</router-link>
                                </li>
                                <li>
                                    <router-link to="/projects">{{locale['link7']}}</router-link>
                                </li>
                                <span v-if="$store.state.userStatus">
                                     <li><router-link to="/webshops/dashboard">Dashboard</router-link></li>
                                     <li @click="logout()"><a>Logout</a></li>
                                </span>
                                <span v-else>
                                    <li><router-link to="/webshops/login">{{locale['link14']}}</router-link></li>
                                </span>
                            </ul>
                        </li>
                        <li v-if="!$store.state.userStatus">
                            <router-link to="/consumers/login">{{locale['link9']}}</router-link>
                        </li>
                        <span v-else>
                            <li><router-link to="/consumers/profile">{{locale['link13']}}</router-link></li>
                            <li @click="logout()"><a>{{locale['link15']}}</a></li>
                        </span>
                        <li>
                            <router-link to="/blogs">{{locale['link10']}}</router-link>
                        </li>
                        <li>
                            <router-link to="/faq">FAQ</router-link>
                        </li>
                        <li>
                            <router-link to="/privacy">{{locale['link12']}}</router-link>
                        </li>
                    </ul>
                </div>
                <div class="uk-width-1-3@m footer-column">
                    <h2 style="margin-bottom: 10px; ">Social</h2>
                    <ul class="social-media-icons">
                        <li><a target="_blank" href="https://www.instagram.com/co2ok.eco/"><i
                                class="fab fa-instagram"></i></a></li>
                        <li><a target="_blank" href="https://www.facebook.com/CO2ok/"><i
                                class="fab fa-facebook-square"></i></a></li>
                        <li><a target="_blank" href="https://twitter.com/CO2ok_eco"><i
                                class="fab fa-twitter-square"></i></a></li>
                        <li><a target="_blank" href="https://www.linkedin.com/company/11418867"><i
                                class="fab fa-linkedin"></i></a></li>
                    </ul>
                </div>
            </div>
        </div>
    </footer>

</template>

<script>
    import axios from 'axios'
    import footerLang from '../../lang/lang_footer'

    export default {
        name: "Footer",

        data() {
            return {
                locale: footerLang
            }
        },

        mounted() {
            this.checkLanguage()
        },


        methods: {
            logout() {
                axios
                    .post('http://127.0.0.1:8000/logout/', {
                        // header: {"X-CSRFToken": 'gZvnzSFeGp7h68WjCzmFky6wMkiJZXDU',}
                    })
                    .then(response => {
                        if (response.data.logout) {
                            this.$store.commit('isLoggedIn', false)
                            this.$store.commit('removeLocalUserData')
                            this.$router.push('/')
                        }
                    })
                    .catch(error => {
                        this.errorMessage()
                    })
            },

            checkLanguage(lang) {
                if(lang === 'en'){
                    this.locale = footerLang.lang_en_footer
                } else {
                    if (this.currentLanguage === 'en') {
                        this.locale = footerLang.lang_en_footer
                    } else {
                        this.locale = footerLang.lang_nl_footer
                    }
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


<style lang="scss">
    #footer /deep/ {
        @import "~uikit/dist/css/uikit.min.css";
    }

    @import '../../styles/layout/main';
    @import '../../styles/layout/footer';
</style>