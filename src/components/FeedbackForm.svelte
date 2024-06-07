        <script>

                    import {v4 as uuidv4} from "uuid"
                    import { listen } from "svelte/internal";
                    import {createEventDispatcher} from 'svelte'
                    import RatingSelect  from "./RatingSelect.svelte"
                    import FeedbackItem  from "./FeedbackItem.svelte"
                    import Button  from "./Button.svelte"
                    import Card  from "./Card.svelte"
                    let text = '';
                    let rating = 10;
                    let message
                    let min = 10
                    let btndisabled  = true

                    const dispatch = createEventDispatcher();
                
                    const handleinput= () => {
                        if(text.trim().length <= min){
                        message = `Number is must be at least ${min} characters`;
                        btndisabled  = true;  
                    }else{
                        message = ``;
                        btndisabled  = false;
                    }
                    }
                
                    const handleselect = e => rating = e.detail

                    const handlesubmit = () => {
                        if(text.trim().length > min){
                            const newFeedback = {
                                id: uuidv4(),
                                text,
                                rating: +rating
                            }
                            // console.log(newFeedback)
                            dispatch('add-feedback', newFeedback);
                            text = ''
                        }
                    }
                    
            
        </script>

        <Card>
            <header>
                <h2>How would you rate your service with us!!</h2>
            </header>
            <form on:submit|preventDefault={handlesubmit}>
            <RatingSelect on:rating-select={handleselect} />
                <div class="input-group">
                    <input type="text"  on:input={handleinput} placeholder="Tell us something" bind:value={text}>
                    <Button disabled={btndisabled}  type="submit">Send</Button>
                </div>
                {#if message}
                <div class="message">
                {message}
                </div>
            {/if}
        </form>

        </Card>
        <style>
            header {
            max-width: 400px;
            margin: auto;
            }
        
            header h2 {
            font-size: 22px;
            font-weight: 600;
            text-align: center;
            }
        
            .input-group {
            display: flex;
            flex-direction: row;
            border: 1px solid #ccc;
            padding: 8px 10px;
            border-radius: 8px;
            margin-top: 15px;
            }
        
            input {
            flex-grow: 2;
            border: none;
            font-size: 16px;
            }
        
            input:focus {
            outline: none;
            }
        
            .message{
            padding-top: 10px;
            text-align: center;
            color: rebeccapurple;
            }
        </style>