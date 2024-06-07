<script>
	import RatingSelect from './components/RatingSelect.svelte'
	import Feedbacklist from './components/FeedbackList.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte'
	import FeedbackForm from './components/FeedbackForm.svelte'

	let feedback = [
		{
    id: 1,
    rating: 10,
    text: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sit, deleniti magnam!",
  },
  {
    id: 2,
    rating: 9,
    text: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sit, deleniti magnam!",
  },
  {
    id: 3,
    rating: 8,
	text: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sit, deleniti magnam!",
  },
	]

	const deleteFeedback = (e) => {
		const itemId = e.detail
		feedback = feedback.filter((item) => item.id != itemId)
	}
	const addFeedback = (e) => {
		const newfeedback = e.detail;
		feedback = [newfeedback, ...feedback]
	}

	$: count = feedback.length
	$: average = feedback.reduce((a,{rating}) => a + rating , 0) / feedback.length || 0
</script>
 
<main class="container">
	<FeedbackForm on:add-feedback={addFeedback}  />
	<FeedbackStats {count} {average}/>
	<Feedbacklist {feedback} on:delete-feedback={deleteFeedback}/>
	<!-- <h1>Hello</h1> -->
</main>


