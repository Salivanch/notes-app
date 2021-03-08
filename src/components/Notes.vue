<template>
    <div class="note_list">

        <div class="note_header">
            <div class="icons">
                <i :class="{active:grid}" @click="grid=true" class="fas fa-border-all icn-choose"></i>
                <i :class="{active:!grid}" @click="grid=false" class="fas fa-bars icn-choose"></i>
            </div>
        </div>

        <div class="notes row row-cols-1 row-cols-md-3 g-4 mt-4 justify-content-center">
            <div :style="{backgroundColor: takeColor(note.priority)}"  :class="{full:!grid}" class="card col-md-5 m-2" v-for="(note) in notes" :key="note.id">
                <div class="card-body">
                    <p class="close" @click="removeNote(note.id)">x</p>
                    <h5 class="card-title" v-if="edit!=note.id" @click="edit=note.id; new_title=note.title">{{note.title}}</h5>
                    <input type="text" v-if="edit==note.id" v-model="new_title" @keydown ="editPress($event, note.id)">
                    <p class="card-text">{{note.descr}}</p>
                    <p class="card-text "><small class="text-muted">{{note.date}}</small></p>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    data (){
        return{
            title: "Notes list",
            grid: true,
            edit: -1,
            new_title: ""
        }
    },
    props: {
        notes: {
            type: Object,
        },
    },
    methods:{
        removeNote (i) {
            this.$emit('remove', i)
        },
        searchNote (val){
            this.$emit('search', val)
        },
        editPress(e, i){
            if (e.keyCode == 27){
                this.new_title = ""
                this.edit = -1
            }
            else if (e.keyCode == 13){
                this.$emit('edit', i, this.new_title)
                this.edit = -1
            }
        },
        takeColor(priority){
            if (priority==1) return "#eaa9be"
            else if (priority==2) return "#dfe890"
            else if (priority==3) return "#80f5a4"
            else return "#fff"
        }

    }
}
</script>

<style scoped>
    input{
        margin: 0 auto;
        display: flex;
        outline: none;
        border: none;
        border-bottom: 1px solid;
        font-weight: 600;
    }
</style>
