<template >
    <Transition name="modal">
        <div class="modal" @click.prevent="$emit('closeModal')">
            <div class="modal__content" @click.stop>
                <h3>{{curNote.id ? words.titlewindowedit[lang] : words.titlewindow[lang]}} </h3>
                <form @submit.prevent="send">
                    <input type="text" :placeholder="words.titlemodal[lang]" required v-model="user.title">
                    <textarea :placeholder="words.contentmodal[lang]" required v-model="user.text"></textarea>
                    <div class="modal__btns">
                        <button type="button" @click.prevent="clean">{{words.closebtn[lang]}}</button>
                        <button>{{curNote.id ? words.editwindowbtn[lang] : words.addbtn[lang]}}</button>
                    </div>
                </form>
            </div>
        </div>
    </Transition> 
</template>
<script>
export default {
    data() {
        return {
            user: {
                title: '',
                text: ''
            }
        }
    },
    methods: {
        send(){
            const note = { ...this.user }
            note.id = this.curNote.id || null
            this.$emit('addNote', note)
            this.clean()
        },
        clean(){
            this.$emit('closeModal')
            for (const key in this.user) this.user[key] = ''
        }
    },
    props: {
        curNote: {
            type: Object,
            default: {}
        },
        lang: {
            type: String,
            default: {}
        }
    },
    watch: {
        curNote(){
            if (this.curNote.id) {
                this.user.title = this.curNote.title
                this.user.text = this.curNote.text
            }
        }
    },
    inject: ['words']
}
</script>
<style lang="scss">
    
</style>