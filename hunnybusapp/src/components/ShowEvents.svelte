

<script>
    export let event
    export let getEvents
    import UpdateEvent from "./UpdateEvent.svelte";
    import axios from 'axios'
	$: showUpdate = false
	
		const revealUpdate = () =>{
			showUpdate=!showUpdate
		}
		  const deleteEvent = async (id) => {
		    await axios.delete('http://localhost:3003/events/' + id).then((response) => {
		        console.log(response)
		        getEvents()
		    })
		  }
</script>
<p>{event.name}</p>
		<p>{event.date}</p>
		<p>{event.address}</p>
		<p>{event.supplies}</p>
		<button on:click={revealUpdate}>Edit</button>
		{#if showUpdate}
		<UpdateEvent  event={event} getEvents={getEvents} revealUpdate={revealUpdate} />
		{/if}
		<form on:submit={()=>deleteEvent(event._id)}>
			<input type="submit" value="delete">
		</form>