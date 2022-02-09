<script>
    import PollStore from '../stores/PollStore';

    import Button from '../components/shared/Button.svelte';
    import { createEventDispatcher } from "svelte";

    let dispatch = createEventDispatcher();

    let fields = {question: '', answerA: '', answerB: ''};
    let errors = {question: '', answerA: '', answerB: ''};
    let valid = false;

    const handleSubmit = () => {
        valid = true;

        //validate question
        if (fields.question.trim().length<5) {
            valid = false;
            errors.question = 'Question must be at least 5 characters long'
        } else {
            errors.question = '';
        }

        //validate answer A
        if (fields.answerA.trim().length<1) {
            valid = false;
            errors.answerA = 'Answer A cannot be empty'
        } else {
            errors.answerA = '';
        }

        //validate answer B
        if (fields.answerB.trim().length<1) {
            valid = false;
            errors.answerB = 'Answer A cannot be empty'
        } else {
            errors.answerB = '';
        }

        // Add a new poll
        if(valid){
            let poll = {...fields, votesA: 0, votesB:0, id: Math.random()}

            //Save poll to store
            PollStore.update(currentPolls => {
                return [poll, ...currentPolls]
            })
            dispatch('add');
        }
    }
</script>

<form on:submit|preventDefault={handleSubmit}>
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" id="question" bind:value={fields.question}/>
        <div class="error">{errors.question}</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A</label>
        <input type="text" id="answer-a" bind:value={fields.answerA}/>
        <div class="error">{errors.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B</label>
        <input type="text" id="answer-a" bind:value={fields.answerB}/>
        <div class="error">{errors.answerB}</div>
    </div> 
    <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
    form{
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field{
        margin: 18px auto;
    }
    input{
        width: 100%;
        border-radius: 6px;
    }
    input{
        width: 100%;
        border-radius: 6px;
    }
    label{
        margin: 10px auto;
        text-align: left;
    }
    .error{
        color: #c41230;
        font-size: 12px;
        font-weight: bold;
    }

</style>