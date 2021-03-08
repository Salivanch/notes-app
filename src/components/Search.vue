<template>
    <div class="note_search">
        <input type="text" v-model="search" class="form-control" placeholder="Find your note"/>
    </div>
</template>

<script>
export default {
    data (){
        return { search: this.value }
    },
    props: {
        value:{
            type: String
        }
    },
    watch: {
        search (val){
            this.$emit('search', val);
        }   
    }
}
</script>

<style scoped>
    .form-control{
        width: 50%;
    }
</style>