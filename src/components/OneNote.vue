<template>
<div class="notes__item">
    <h3>{{note.title}}</h3>
    <span>{{note.date}}</span>
    <p>{{note.text}}</p>
    <div class="notes__control">
        <a href="#" @click.prevent="$emit('edit', note)"><img src="@/assets/img/edit.svg" alt="">{{words.editbtn[lang]}}</a>
        <a href="#" @click.prevent="$emit('remove', note.id)"><img src="@/assets/img/del.svg" alt="">{{words.deledit[lang]}}</a>
    </div>
</div>
</template>
<script>
export default {
    props: {
        note: {
            type: Object,
            default: {}
        },
        lang: {
            type: String,
            default: ''
        }
    },    
    inject: ['words']
}
</script>
<style lang="scss">
    
</style>