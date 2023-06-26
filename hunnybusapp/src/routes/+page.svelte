
        <script>
        import { onMount } from 'svelte'
		import { Accordion, AccordionItem } from '@skeletonlabs/skeleton'
		import { Datepicker } from 'svelte-calendar'
		import axios from 'axios'
		
		let eventsArray = []
		
		let number = 0
		
		const clickCount = () => {
	        number += 1
		    return number
		  }
		  onMount( async () => {
		    const response = await fetch('http://localhost:3003/events')
		     eventsArray = await response.json()
		    console.log(eventsArray)
		  })
		</script>
		<div id="logo">
		<img class="" src="./hunnybuslogo.webp" alt="">
		</div>
		<button on:click={clickCount}>{number}</button>
		{#each eventsArray as event}
		<p>{event.name}</p>
		{/each}
		<Accordion>
		    <AccordionItem open>
		        <svelte:fragment slot="summary">Hello</svelte:fragment>
		    </AccordionItem>
		</Accordion>
		<Datepicker />
        <style>
        #logo{
        display: flex;
        justify-content: center;
        }
        </style>