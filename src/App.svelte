<script>
  let i = 0
  let points = 0
  let input = ''
  let lower = ''
  let name = ''
  let age = 0 
  let named = false
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
    
    {question:"Forward I am heavy, but backwards I am not. What am I?",
    type:"multi",
    a1:"elephant",
    a2:"ton",
    a3:"gravity",
    a4:"God",
    answer:"ton",
    selection:"", 
    result:""},

    {question:"What can fill a room but takes up no space?",
    type:"multi",
    a1:"silence",
    a2:"air",
    a3:"elephant",
    a4:"light",
    answer:"light",
    selection:"", 
    result:""},

    {question:"I have lakes with no water, mountains with no stone and cities with no buildings. What am I?",
    type:"multi",
    a1:"dream",
    a2:"map",
    a3:"painting",
    a4:"song",
    answer:"map",
    selection:"", 
    result:""},

    {question:"What goes through cities and fields, but never moves?",
    type:"multi",
    a1:"road",
    a2:"sky",
    a3:"ground",
    a4:"time",
    answer:"road",
    selection:"", 
    result:""},

    {question:"A man looks at a painting in a museum and says, “Brothers and sisters I have none, but that man’s father is my father’s son.” Who is in the painting?",
    type:"multi",
    a1:"The man's grandfather",
    a2:"The man's uncle",
    a3:"The man's son",
    a4:"The man's father",
    answer:"The man's son",
    selection:"", 
    result:""},

    {question:"What three numbers, none of which is zero, give the same result whether they’re added or multiplied?",
    type:"multi",
    a1:"2, 3, and 4",
    a2:"2, 3, and 5",
    a3:"1, 2, and 3",
    a4:"1, 2, and 4",
    answer:"1, 2, and 3",
    selection:"", 
    result:""},

    {question:"Mary has four daughters, and each of her daughters has a brother. How many children does Mary have?",
    type:"multi",
    a1:"10",
    a2:"8",
    a3:"4",
    a4:"5",
    answer:"5",
    selection:"", 
    result:""},

    {question:"What has many teeth but can't bite?",
    type:"word",
    answer:"comb",
    selection:"",
    result:""},

    {question:"What begins with an 'e' and only contains one letter?",
    type:"word",
    answer:"envelope",
    selection:"",
    result:""},

    {question:"What is so fragile that saying its name breaks it?",
    type:"word",
    answer:"silence",
    selection:"",
    result:""},

    {question:"If you drop me I’m sure to crack, but give me a smile and I’ll always smile back. What am I?",
    type:"word",
    answer:"mirror",
    selection:"",
    result:""},

    {question:"The more you take, the more you leave behind.",
    type:"word",
    answer:"footsteps",
    selection:"",
    result:""},

    {question:"Which is heavier: a ton of bricks or a ton of feathers?",
    type:"word",
    answer:"neither both",
    selection:"",
    result:""},

    {question:"What is black when it’s clean and white when it’s dirty?",
    type:"word",
    answer:"a blackboard",
    selection:"",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"",
    type:"word",
    answer:"",
    selection:"",
    result:""},

    {question:"If there are three apples and you take away two, how many apples do you have?",
    type:"number",
    answer:"2",
    selection:"",
    result:""},
  ]
    let questions = library.sort(function(a, b){return 0.5 - Math.random()});
    questions.splice(3, questions.length)

let leaderboard = [

]
function submit(){
  input = questions[i].selection
  lower = input.toLowerCase()
  answering = false
  if (questions[i].type == 'word'){
    if (questions[i].answer.includes(lower)){
    questions[i].result = 'Correct'
    points += 1
    } else {
    questions[i].result = "Wrong. The correct answer was '" + questions[i].answer + "'."
    }
  } else {
    if (questions[i].selection == questions[i].answer){
    questions[i].result = 'Correct'
    points += 1
    } else {
    questions[i].result = "Wrong. The correct answer was '" + questions[i].answer + "'."
    }
  }
  
}
function next(){
  i += 1
  answering = true
}
function reset(){
  leaderboard.splice(leaderboard.length, 0, {name:name, age:age, points:points})
  i = 0
  points = 0
  answering = true
  named = false
  for (let r = 0; r < questions.length; r++) {
        questions[r].selection = ""
        questions[r].result = ""
      }
 
}
function begin(){
  named = true
}
</script>

<h1>Riddles</h1>
{#if named}
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
    <br>
    Leaderboard:
    <br>
    {#each leaderboard as score}
    Name: {score.name}
    Age: {score.age}
    Score: {score.points} / {questions.length}
    <br>
    {/each}
  {/if}
{:else}
  <label>
  Name:
  <input type="text" bind:value={name}>
  </label>
  <br>
  <label>
  Age:
  <input type="number" bind:value={age}>
  </label>
  <button on:click={begin}>
    Submit
  </button>
{/if}


