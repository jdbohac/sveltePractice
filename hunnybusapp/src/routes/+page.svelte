
        <script>
        
		import { Accordion, AccordionItem } from '@skeletonlabs/skeleton'
		import { Datepicker } from 'svelte-calendar'
		let number = 0

		const clickCount = () => {
	        number += 1
		    return number
		  }
		</script>
		<div id="logo">
		<img class="" src="./hunnybuslogo.webp" alt="">
		</div>
		<button on:click={clickCount}>{number}</button>
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