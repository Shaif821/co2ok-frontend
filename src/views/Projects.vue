<template>
    <div>
        <Header :image="header"></Header>

        <div class="uk-section cause__sect-1">
            <div class="uk-container uk-container-column uk-container-width">
                <div class="sect-1-col-1">
                    <div class="img-wrapper-1 uk-box-shadow-medium">
                        <img class="sect-1__img-1" src="../assets/images/projects/project-1.png" alt="project 1">
                    </div>

                    <p class="main-text">
                        {{locale['section1_text']}}
                    </p>

                    <div class="img-wrapper-2 uk-box-shadow-medium">
                        <img class="sect-1__img-2" src="../assets/images/projects/project-2.png" alt="project 2">
                    </div>
                </div>

                <div class="sect-1-col-2">
                    <div class="second-img-wrapper-1 hide-desktop">
                        <img class="sect-1__img-3 responsive-img  uk-box-shadow-medium" src="../assets/images/projects/project-1.png" alt="project 1">
                    </div>

                    <div class="second-img-wrapper-2 hide-desktop">
                        <img class="sect-1__img-4 responsive-img uk-box-shadow-medium" src="../assets/images/projects/project-2.png" alt="project 1">
                    </div>

                    <div class="second-img-wrapper-1">
                        <img class="sect-1__img-3 responsive-img uk-box-shadow-medium" src="../assets/images/projects/project-3.png" alt="project 1">
                    </div>

                    <div class="second-img-wrapper-2">
                        <img class="sect-1__img-4 responsive-img uk-box-shadow-medium" src="../assets/images/projects/project-4.png" alt="project 1">
                    </div>
                </div>
            </div>
        </div>


        <div class="uk-section cause__sect-2">
            <div class="uk-container uk-container-row uk-container-width">
                <div class="sect-2-col-1">
                    <div class="content-intro">
                        <h3 class="sub-title">{{locale['section2_subTitle']}}</h3>
                        <h2 class="main-title">{{locale['section2_title']}}</h2>
                        <p class="main-text">
                            {{locale['section2_text']}}
                        </p>

                    </div>

                    <div class="content-row">
                        <div class="row-item">
                            <h3 class="row-title"><i class="fas fa-wind subheading"></i> {{locale['s2_title1']}}</h3>
                            <p>
                                {{locale['s2_text1']}}
                            </p>
                        </div>

                        <div class="row-item">
                            <h3 class="row-title"><i class="fas fa-solar-panel subheading"></i> {{locale['s2_title2']}}</h3>
                            <p>{{locale['s2_text2']}}</p>
                        </div>

                        <div class="row-item">
                            <h3 class="row-title"><i class="fas fa-tint subheading"></i> {{locale['s2_title3']}}</h3>
                            <p>{{locale['s2_text3']}}</p>
                        </div>
                    </div>
                </div>

                <div class="sect-2-col-2">
                    <img class="sect-2__img-1  uk-box-shadow-medium" src="../assets/images/projects/project-5.png">
                </div>
            </div>
        </div>


        <div class="uk-section cause__sect-2">
            <div class="uk-container uk-container-row row-reverse uk-container-width">
                <div class="sect-2-col-1">
                    <div class="content-intro">
                        <h3 class="sub-title">{{locale['section3_subTitle']}}</h3>
                        <h2 class="main-title">{{locale['section3_title']}}</h2>
                        <p class="main-text">
                            {{locale['section3_text']}}
                        </p>

                    </div>

                    <div class="content-row">
                        <div class="row-item">
                            <h3 class="row-title"><i class="fas fa-utensils subheading"></i> {{locale['s3_title1']}}</h3>
                            <p>
                                {{locale['s3_text1']}}
                            </p>
                        </div>

                        <div class="row-item">
                            <h3 class="row-title"><i class="far fa-sun subheading"></i> {{locale['s3_title2']}}</h3>
                            <p>{{locale['s3_text2']}}</p>
                        </div>

                        <div class="row-item row-item__width">
                            <h3 class="row-title">{{locale['s3_title3']}}</h3>
                            <p>{{locale['s3_text3']}}</p>
                        </div>
                    </div>
                </div>

                <div class="sect-2-col-2 to-left">
                    <img class="sect-2__img-1  uk-box-shadow-medium" src="../assets/images/projects/project-6.png">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    const Header = () => import('@/components/layout/Header')
    import projectsLang from '../lang/lang_projects'


    export default {
        name: "Projects",
        components: {'Header': Header},

        data() {
            return {
                header: 'projects',
                locale: projectsLang,
            }
        },

        mounted() {
            this.checkLanguage()
        },

        methods: {
            checkLanguage(lang) {
                if(lang === 'en'){
                    this.locale = projectsLang.lang_en_projects
                } else {
                    if (this.currentLanguage === 'en') {
                        this.locale = projectsLang.lang_en_projects
                    } else {
                        this.locale = projectsLang.lang_nl_projects
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

<style lang="scss" scoped>
    @import '../styles/layout/main.scss';
    @import '../styles/projects.scss';
</style>