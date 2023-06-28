<script>
export let getEvents
export let event
export let revealUpdate
import axios from 'axios'
    import { writable } from 'svelte/store';
        let updatedEvent = {...event}
		  const handleChange = (e) => {
		    updatedEvent = {...updatedEvent, [e.target.name]: e.target.value }
		  }
		  const updateEvent = async  () => {
			  await axios.put('http://localhost:3003/events/' + event._id, updatedEvent).then((response) =>{
			    console.log(response)
			    getEvents()
			    document.getElementById('updateForm').reset()
			    revealUpdate()
		  })
		  }
</script>

<div>
		<form class="form-container" id="updateForm" on:submit={updateEvent}>
			<label for="name">Client Name(s)</label>
			<input type="text" name="name" id="name" value={updatedEvent.name} on:change={handleChange}>
			<input type="date" name="date" id="date" value={updatedEvent.date} on:change={handleChange}>
			<label for="address">Venue Address</label>
			<input type="text" name="address" id="address" value={updatedEvent.address} on:change={handleChange}>
			<label for="supplies">supplies needed</label>
			<textarea name="supplies" rows="4" id="supplies" value={updatedEvent.supplies} on:change={handleChange}></textarea>
			<input type="submit">
		</form>
	</div>
	<style>
	
        .form-container{
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: left;
        }
	</style>