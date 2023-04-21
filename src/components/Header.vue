<template>
    <header class="header">
        <Transition name="header-change" mode="out-in">
            <div class="header__notes" v-if="header">
            <button @click="changeLang">{{ lang == 'ru' ? 'RU' : 'UZ'}}</button>
            <h1>{{words.appbartitle[lang]}}</h1>
            <button @click="header = false"><img src="@/assets/img/search.svg" alt=""></button>
        </div>
        <form class="header__form" v-else>
            <a href="#" class="back" @click.prevent="header = true, search = ''"><img src="@/assets/img/back.svg" alt=""></a>
            <input type="text" :placeholder="words.appbarseacrch[lang]" required name="search" v-model="search">
            <a href="#" class="close" @click.prevent ="search = ''"><img src="@/assets/img/close.svg" alt=""></a>
        </form>
        </Transition>
    </header>
</template>
<script>
export default {
    data() {
        return {
            header: true,
            search: ''
        }
    },
        props:  {
            lang: {
                type: String,
                default: ''
            }
        },
    watch: {
        search (val){
            this.$emit('find', val)
        }
    },
    methods: {
        changeLang(){
            this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru')
        }
    },
    inject: ['words']
}
</script>
<style lang="scss">
.header-change-enter-active,
.header-change-leave-active {
  transition: opacity 0.5s ease;
}

.header-change-enter-from,
.header-change-leave-to {
  opacity: 0;
}

</style>