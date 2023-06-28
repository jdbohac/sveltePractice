<script>
export let getEvents
import axios from 'axios'
    import { writable } from 'svelte/store';
        let event = {
			name: String,
			date: Date,
			address: String,
			supplies: String
		}
		  const handleChange = (e) => {
		    event = {...event, [e.target.name]: e.target.value }
		  }
		  const addEvent = async  () => {
			  await axios.post('http://localhost:3003/events', event).then((response) =>{
			    console.log(response)
			    getEvents()
			    document.getElementById('addForm').reset()
		  })
		  }
</script>

<div>
		<form class="form-container" id="addForm" on:submit={addEvent}>
			<label for="name">Client Name(s)</label>
			<input type="text" name="name" id="name" on:change={handleChange}>
			<input type="date" name="date" id="date" on:change={handleChange}>
			<label for="address">Venue Address</label>
			<input type="text" name="address" id="address" on:change={handleChange}>
			<label for="supplies">supplies needed</label>
			<textarea name="supplies" rows="4" id="supplies" on:change={handleChange}></textarea>
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