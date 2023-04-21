<template>
   <div class="notes">
        <div class="container">
            <div class="notes__nav">
                <h2 v-if="notes.length > 0">{{ !search ? words.infobar[lang] : words.appbarseacrch[lang]}}</h2>
                <h2 v-else>{{ words.noinfobar[lang] }}</h2>
                <button @click="grid = !grid">
                    <img src="@/assets/img/list.svg" alt="" v-if = grid>
                    <img src="@/assets/img/grid.svg" alt="" v-else>
                    <span>{{grid ? words.list[lang] : words.grid[lang]}}</span>
                </button>
            </div>
            <transition-group tag="div" class="notes__grid" :class="{list: !grid}" name="notes">
            <OneNote 
            v-for="note in notes" :key="note.id" 
            :note="note"
            :lang="lang" 
            @remove="$emit('remove', note.id)"
            @edit="$emit('edit', note)"
        />
            </transition-group>
        </div>
   </div>
</template>
<script>
import OneNote from './OneNote.vue'
export default {
  components: { OneNote },
    data() {
        return {
            grid: true
        }
    },
    props: {
        notes: {
            type: Array,
            default: []
        },
        search: {
            type: String,
            default: ''
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