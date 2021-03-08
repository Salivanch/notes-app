<template>
    <div class="container">
        <h1>{{title}}</h1>

		<message v-if="message" :message="message" />
		<newNote :note="note" :message="message" @addNote="addNote" />
		<h2 class="mt-5">Notes list</h2>
		<search :value="search" @search="search=$event" />
		<notes 
			v-if="notes.length > 0" 
			:notes="notesFilter" 
			@remove="removeNote"
			:value="serach"
			@edit="editNote"
		/>
	</div>


</template>

<script>
	import message from '@/components/Message.vue'
	import newNote from '@/components/NewNote.vue'
	import search from '@/components/Search.vue'
	import notes from '@/components/Notes.vue'

	export default {
		name: 'App',
		components: {message, newNote, search, notes},
		data () {
			return {
				message: null,
				search: "",
				note:{
					title: '',
					descr: '',
					priority: '',
				},
				title: "Notes App",
				notes: [
					{
						id: 0,
						title: 'First Note',
						descr: 'Description for first note',
						date: new Date(Date.now()).toLocaleString(),
						priority: '3',
					},
					{
						id: 1,
						title: 'Second Note',
						descr: 'Description for second note',
						date: new Date(Date.now()).toLocaleString(),
						priority: '3',
					}
				]
			}
		},
		methods: {
			addNote(){
				let {title, descr, priority} = this.note,
					id = this.notes.length
				
				if (title === ''){
					this.message = "Данное поле не может быть пустым"
					return false
				}

				this.notes.push({
					id,
					title,
					descr,
					priority,
					'date': new Date(Date.now()).toLocaleString(),
				})

				this.note.title = ""
				this.note.descr = ""
				this.message = ""
			},
			removeNote(index){
				this.notes.splice(index, 1);
			},
			editNote(index, new_title){
				this.notes[index].title = new_title
				this.notes[index].date = new Date(Date.now()).toLocaleString()
			}
		},
		computed: {
			notesFilter (){
				let array = this.notes,
					search = this.search;
				if (!search) return array
				//small
				search = search.trim().toLowerCase()
				//filter
				array = array.filter((item)=>{
					if (item.title.toLowerCase().indexOf(search) != -1){
						return item
					}
				})
				return array
			}
		}
	}
</script>


<style>
</style>
