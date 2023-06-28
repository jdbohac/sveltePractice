
        <script>
        import { onMount } from 'svelte'
		import { Accordion, AccordionItem } from '@skeletonlabs/skeleton'
		import { Datepicker } from 'svelte-calendar'
		import axios from 'axios'
		
		let eventsArray = []
		
		let number = 0
		
		let event = {
			name: String,
			date: Date,
			address: String,
			supplies: String
		}
		
		const clickCount = () => {
	        number += 1
		    return number
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
		  const deleteEvent = async (id) => {
		    await axios.delete('http://localhost:3003/events/' + id).then((response) => {
		        console.log(response)
		        onMount()
		    })
		  }
		  onMount(async() => {
		  const response = await fetch('http://localhost:3003/events')
		    eventsArray = await response.json()
		  })
		</script>
		<div id="logo">
		<img class="" src="./hunnybuslogo.webp" alt="">
		</div>
		<button on:click={clickCount}>{number}</button>
		{#each eventsArray as event (event._id)}
		<p>{event.name}</p>
		<p>{event.date}</p>
		<p>{event.address}</p>
		<p>{event.supplies}</p>
		<form on:submit={()=>deleteEvent(event._id)}>
			<input type="submit" value="delete">
		</form>
		{/each}
		<Accordion>
		    <AccordionItem open>
		        <svelte:fragment slot="summary">Hello</svelte:fragment>
		    </AccordionItem>
		</Accordion>
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
        #logo{
        display: flex;
        justify-content: center;
        }
        .form-container{
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        </style>