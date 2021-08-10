<script>
  let i = 0
  let points = 0
  let answering = true
  let library = [
    {question:"I am an odd number. Take away a letter and I become even. What am I?",
    type:"multi",
    a1:"3",
    a2:"5",
    a3:"7",
    a4:"9",
    answer:"7",
    selection:"", 
    result:""},

    {question:"What has many teeth but can't bite?",
    type:"word",
    answer:"comb",
    selection:"",
    result:""},

    {question:"If there are three apples and you take away two, how many apples do you have?",
    type:"number",
    answer:"2",
    selection:"",
    result:""},
  ]
    let questions = library.sort(function(a, b){return 0.5 - Math.random()});
    questions.splice(2, questions.length)
function submit(){
  answering = false
  if (questions[i].selection == questions[i].answer){
    questions[i].result = 'Correct'
    points += 1
  } else {
    questions[i].result = "Wrong. The correct answer was '" + questions[i].answer + "'."
  }
}
function next(){
  i += 1
  answering = true
}
function reset(){
  i = 0
  points = 0
  answering = true
  for (let r = 0; r < questions.length; r++) {
        questions[r].selection = ""
        questions[r].result = ""
      }
 
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
{:else if (questions[i].type == 'word')}
<input type="text" bind:value={questions[i].selection}>
{:else if (questions[i].type == 'number')}
<input type="number" bind:value={questions[i].selection}>
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
Well done, you got {points} / {questions.length}!
<button on:click={reset}>
  Play again
</button>
{/if}



