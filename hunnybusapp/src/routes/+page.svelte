
		<script>
		  import Home from './home/Home.svelte'
		  import Events from './events/Events.svelte'
		  import Router from 'svelte-spa-router';
		  import NotFound from './not_found/NotFound.svelte';

		  let routes = {
		    '/': Home,
		    '/events/:id': Events,
		    
		    '*': NotFound
		  }
		</script>
		
		  <Router {routes} />
		  
		