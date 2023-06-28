<script>
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
			    eventsArray.push(event)
		  })
		  }
</script>

<div>
		<form class="form-container" on:submit={addEvent}>
			<label for="name">Client Name(s)</label>
			<input type="text" name="name" on:change={handleChange}>
			<input type="date" name="date" on:change={handleChange}>
			<label for="address">Venue Address</label>
			<input type="text" name="address" on:change={handleChange}>
			<label for="supplies">supplies needed</label>
			<textarea name="supplies" rows="4" on:change={handleChange}></textarea>
			<input type="submit">
		</form>
	</div>
	<style>
	
        .form-container{
            display: flex;
            flex-direction: column;
            align-items: center;
        }
	</style>