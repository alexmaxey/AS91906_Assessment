<script>
  let i = 0
  let points = 0
  let answering = true
    let questions = [
    {question:"I am an odd number. Take away a letter and I become even. What am I?",
    type:"multi",
    a1:"3",
    a2:"5",
    a3:"7",
    a4:"9",
    selection:"",
    answer:"7",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"",
    type:"number",
    answer:"",
    selection:"",
    result:""},
  ]
function submit(){
  answering = false
  if (questions[i].selection == questions[i].answer){
    questions[i].result = 'Correct'
    points += 1
  } else {
    questions[i].result = 'Wrong'
  }
}
function next(){
  i += 1
  answering = true
}
</script>

<h1>Riddles</h1>
{#if (i < questions.length)}
{questions[i].question}
<br>
{#if (questions[i].type == 'multi')}
<label>
  <input type="radio" bind:group={questions[i].selection} value={questions[i].a1}>
  {questions[i].a1}
</label>
<br>
<label>
  <input type="radio" bind:group={questions[i].selection} value={questions[i].a2}>
  {questions[i].a2}
</label>
<br>
<label>
  <input type="radio" bind:group={questions[i].selection} value={questions[i].a3}>
  {questions[i].a3}
</label>
<br>
<label>
  <input type="radio" bind:group={questions[i].selection} value={questions[i].a4}>
  {questions[i].a4}
</label>
{/if}
<br>
{questions[i].result}
<br>
{#if answering}
<button on:click={submit}>
  Submit
</button>
{:else}
<button on:click={next}>
  Next
</button>
{/if}
{:else}
You got {points} / {questions.length}
{/if}



