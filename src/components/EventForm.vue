<template>
    <b-modal id="modalEvent" ref="modalEvent" size="sm" hide-header hide-footer>
        <h3>Add an event to your calendar</h3>
        <br/>
        <b-form-input type="text" id="event-title" v-model="eventTitle" placeholder="Give your event a title"/>
        <br/>
        <b-form-input type="text" id="event-desc" v-model="eventDesc" placeholder="Give your event a description"/>
        <br/>
        <label for="eventStartdate">When your event should start?</label>
        <b-form-input type="date" id="event-startdate" v-model="eventStartdate"/>
        <br/>
        <label for="event-enddate">When your event should end?</label>
        <b-form-input type="date" id="event-enddate" v-model="eventEnddate" placeholder="When your event should end?"/>
        <br/>
        <b-button variant="outline-primary" block @click="addEvent">Add your event!</b-button>
        <b-button variant="outline-danger" block @click="hideModal">Cancel</b-button>
    </b-modal>
</template>

<script>
    export default {
        name: "EventForm",
        data () {
            return {
                eventTitle:'',
                eventDesc:'',
                eventStartdate:'',
                eventEnddate:''
            }
        },
        methods: {
            hideModal(){
                this.$refs.modalEvent.hide()
            },
            addEvent(){
                const p = new URLSearchParams()
                p.set('title', this.eventTitle)
                p.set('desc', this.eventDesc)
                p.set('startDate', this.eventStartdate)
                p.set('endDate', this.eventEnddate)
                this.$axios.post('/add', p)
                    .then(response => this.onSuccess(response))
                    .catch(() => console.log('error'))
            },
            onSuccess(response){
                console.log(response)
                this.hideModal()
                this.$emit('add')
            }
        }
    }
</script>

<style scoped>

</style>
