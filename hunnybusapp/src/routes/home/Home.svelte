
    <script>
        import { onMount } from 'svelte'
		import { Accordion, AccordionItem } from '@skeletonlabs/skeleton'
		import AddAppointment from '../../components/AddAppointment.svelte'
		import axios from 'axios'
		import Router from 'svelte-spa-router'
    import ShowEvents from '../../components/ShowEvents.svelte'
		
		$: eventsArray = []
		let number = 0
		const clickCount = () => {
	        number += 1
		    return number
		  }
		  $: getEvents = async () => {
		  eventsArray = []
		   const response = await fetch('http://localhost:3003/events')
		    eventsArray = await response.json()
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
		<ShowEvents {event} {getEvents} />
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