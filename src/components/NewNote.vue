<template >
    <form class="new_note">
        <div class="form-floating mb-3">
            <input type="text" class="form-control" id="floatingInput" v-model="note.title" :class="message ? 'border-danger' : '' ">
            <label for="floatingInput">Title</label>
        </div>
        <div class="form-floating mb-3">
            <textarea class="form-control" placeholder="Leave a comment here" id="floatingTextarea" v-model="note.descr"></textarea>
            <label for="floatingTextarea">Description</label>
        </div>
        <div>
            <span>Приоритет выполнения: </span>
            <div class="form-check form-check-inline">
                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="1" v-model="note.priority">
                <label class="form-check-label" for="inlineRadio1">1</label>
            </div>
            <div class="form-check form-check-inline">
                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="2" v-model="note.priority">
                <label class="form-check-label" for="inlineRadio2">2</label>
            </div>
            <div class="form-check form-check-inline">
                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio3" value="3" v-model="note.priority">
                <label class="form-check-label" for="inlineRadio3">3</label>
            </div>
        </div>
        <button type="button" class="btn btn-primary" @click="addNote">Добавить</button>
    </form>
</template>


<script>
	export default {
        props:{
            note:{
                type: Object,
            },
            message: {
                type: String,
            },
        },
        methods: {
            addNote (){
                this.$emit('addNote', this.note)
            }
        }
	}
</script>

<style scoped>
    form{
        margin: 0 auto;
        max-width: 600px;
    }
    button{
        display: block;
        margin: 10px auto;
        width: 30%;
    }
    span{
        font-size: 17px;
        position: relative;
        top: -1px;
        margin: 0px 5px;
        font-weight: 500;
    }
</style>