<script>
    import {v4 as uuidv4} from 'uuid'
    import Card from './Card.svelte'
    import Button from './Button.svelte'
    import RatingSelect from './RatingSelect.svelte'
    import {createEventDispatcher} from 'svelte'

    let dispatch = createEventDispatcher();
    let rating = 10
    let btnDisabled = true
    let text=''
    let min  =10
    let message = ''
    const handleInput = ()=>{
        if(text.trim().length<=min){
            message = `Text must be atleast ${min} characters`
            btnDisabled = true
        }else{
            message = null
            btnDisabled = false
        }
    }

    const handleSelect = e => rating = e.detail;
    const handleSubmit = ()=>{
        if(text.trim().length > min){
            const newFeedback = {
                text,
                rating: +rating,
                id: uuidv4()
            }
            // console.log(newFeedback)
            dispatch('add-feedback',newFeedback)
            text=""
        }
    }
</script>

<Card>

    <header>
        <h2>How would you rate your service with us?</h2>
    </header>
<form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleSelect}/>
    <div class="input-group">
        <input type="text" on:input={handleInput} bind:value={text} placeholder="Tell us something that keeps you coming back">
        <Button type="submit" disabled={btnDisabled}>Send</Button>
    </div>
   {#if message}
    <div class="message">
        {message}
    </div>
   {/if}
</form>
</Card>

<style>
    h2{
        text-align: center;
    }
    .input-group{
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .input-group input{
        width : 80%;
        padding: 1em 1em;
        border-radius: 0.7em;
        border: 1px solid black;
        font-size: 1em;
    }
    .message{
        color:#121212;
        text-align: center;
        padding: 10px;
    }
</style>