<script>
	import FeedbackList from './Components/FeedbackList.svelte'
	import FeedbackStats from './Components/FeedbackStats.svelte'
	import FeedbackForm from './Components/FeedbackForm.svelte'
	let id = 0
	let feedback = [
		{
			id: id++,
			rating: 9,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda dolorum harum doloribus quis ex in accusantium ipsum, voluptates at magni.'
		},
		{
			id: id++,
			rating:5,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda dolorum harum doloribus quis ex in accusantium ipsum, voluptates at magni.'
		},
		{
			id: id++,
			rating: 7,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda dolorum harum doloribus quis ex in accusantium ipsum, voluptates at magni.'
		},
	]

	$: count = feedback.length
	$:average = (feedback.reduce((a,{rating})=>a+rating,0)/count).toFixed(2)

	const deleteFeedback = (e)=>{
		// console.log(e.detail);
		const itemId = e.detail
		feedback = feedback.filter((item)=>item.id!=itemId)
	}

	const addFeedback = e=>{
		feedback = [ e.detail,...feedback,]
	}
</script>

<main class="container">
	<FeedbackForm on:add-feedback={addFeedback}/>
	<FeedbackStats {count} {average}/>
	<FeedbackList {feedback} on:delete-feedback={deleteFeedback}/>
</main>

