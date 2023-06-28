
    <script>
        import { onMount } from 'svelte'
		import { Accordion, AccordionItem } from '@skeletonlabs/skeleton'
		import AddAppointment from '../components/AddAppointment.svelte'
		import { Datepicker } from 'svelte-calendar'
		import axios from 'axios'
        import UpdateEvent from '../components/UpdateEvent.svelte';
		
		$: eventsArray = []
		$: showUpdate = false
		let number = 0
		const revealUpdate = () =>{
			showUpdate=!showUpdate
		}
		const clickCount = () => {
	        number += 1
		    return number
		  }
		  $: getEvents = async () => {
		  eventsArray = []
		   const response = await fetch('http://localhost:3003/events')
		    eventsArray = await response.json()
		  }
		  const deleteEvent = async (id) => {
		    await axios.delete('http://localhost:3003/events/' + id).then((response) => {
		        console.log(response)
		        getEvents()
		    })
		  }
		  onMount(async() => {
		    getEvents()
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
		<button on:click={revealUpdate}>Edit</button>
		{#if showUpdate}
		<UpdateEvent  event={event} getEvents={getEvents} revealUpdate={revealUpdate} />
		{/if}
		<form on:submit={()=>deleteEvent(event._id)}>
			<input type="submit" value="delete">
		</form>
		{/each}
		<Accordion>
		    <AccordionItem open>
		        <svelte:fragment slot="summary">Hello</svelte:fragment>
		    </AccordionItem>
		</Accordion>
		<AddAppointment getEvents={getEvents} />
        <style>
        #logo{
        display: flex;
        justify-content: center;
        }
        </style>