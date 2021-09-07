<script>
  let i = 0
  let points = 0
  let input = ''
  let lower = ''
  let name = ''
  let first_time = true
  let age = 0 
  let game_length = 3
  let named = false
  let error_message = ''
  let answering = true
  let questions = []
  let library = []
  let leaderboard = []

// Shuffles the questions randomly and cuts them to the game length
function shuffle(){
  questions = []
    library = [
    {question:"I am an odd number. Take away a letter and I become even. What am I?",
    type:"multi",
    a1:"3",
    a2:"5",
    a3:"7",
    a4:"9",
    answer:"7",
    selection:"", 
    result:"", 
    number:"1"},
    
    {question:"Forward I am heavy, but backwards I am not. What am I?",
    type:"multi",
    a1:"elephant",
    a2:"ton",
    a3:"gravity",
    a4:"God",
    answer:"ton",
    selection:"", 
    result:"",
    number:"2"},

    {question:"What can fill a room but takes up no space?",
    type:"multi",
    a1:"silence",
    a2:"air",
    a3:"elephant",
    a4:"light",
    answer:"light",
    selection:"", 
    result:"",
    number:"3"},

    {question:"I have lakes with no water, mountains with no stone and cities with no buildings. What am I?",
    type:"multi",
    a1:"dream",
    a2:"map",
    a3:"painting",
    a4:"song",
    answer:"map",
    selection:"", 
    result:"",
    number:"4"},

    {question:"What goes through cities and fields, but never moves?",
    type:"multi",
    a1:"road",
    a2:"sky",
    a3:"ground",
    a4:"time",
    answer:"road",
    selection:"", 
    result:"",
    number:"5"},

    {question:"A man looks at a painting in a museum and says, “Brothers and sisters I have none, but that man’s father is my father’s son.” Who is in the painting?",
    type:"multi",
    a1:"The man's grandfather",
    a2:"The man's uncle",
    a3:"The man's son",
    a4:"The man's father",
    answer:"The man's son",
    selection:"", 
    result:"",
    number:"6"},

    {question:"What three numbers, none of which is zero, give the same result whether they’re added or multiplied?",
    type:"multi",
    a1:"2, 3, and 4",
    a2:"2, 3, and 5",
    a3:"1, 2, and 3",
    a4:"1, 2, and 4",
    answer:"1, 2, and 3",
    selection:"", 
    result:"",
    number:"7"},

    {question:"Mary has four daughters, and each of her daughters has a brother. How many children does Mary have?",
    type:"multi",
    a1:"10",
    a2:"8",
    a3:"4",
    a4:"5",
    answer:"5",
    selection:"", 
    result:"",
    number:"8"},

    {question:"What has many teeth but can't bite?",
    type:"word",
    answer:"comb",
    selection:"",
    result:"",
    number:"9"},

    {question:"What begins with an 'e' and only contains one letter?",
    type:"word",
    answer:"envelope",
    selection:"",
    result:"",
    number:"10"},

    {question:"What is so fragile that saying its name breaks it?",
    type:"word",
    answer:"silence",
    selection:"",
    result:"",
    number:"11"},

    {question:"If you drop me I’m sure to crack, but give me a smile and I’ll always smile back. What am I?",
    type:"word",
    answer:"mirror",
    selection:"",
    result:"",
    number:"12"},

    {question:"The more you take, the more you leave behind.",
    type:"word",
    answer:"footsteps",
    selection:"",
    result:"",
    number:"13"},

    {question:"Which is heavier: a ton of bricks or a ton of feathers?",
    type:"word",
    answer:"neither",
    selection:"",
    result:"",
    number:"14"},

    {question:"What is black when it’s clean and white when it’s dirty?",
    type:"word",
    answer:"blackboard",
    selection:"",
    result:"",
    number:"15"},

    {question:"What is full of holes but still holds water?",
    type:"word",
    answer:"sponge",
    selection:"",
    result:"",
    number:"16"},

    {question:"What is always infront of you but can't be seen?",
    type:"word",
    answer:"future",
    selection:"",
    result:"",
    number:"17"},

    {question:"What goes up but never comes down?",
    type:"word",
    answer:"age",
    selection:"",
    result:"",
    number:"18"},

    {question:"The more of this there is, the less you see. What is it?",
    type:"word",
    answer:"darkness",
    selection:"",
    result:"",
    number:"19"},

    {question:"What has one eye but can't see?",
    type:"word",
    answer:"needle",
    selection:"",
    result:"",
    number:"20"},


    {question:"What has hands, but can't clap?",
    type:"word",
    answer:"clock",
    selection:"",
    result:"",
    number:"21"},
  ]
  questions = library.sort(function(a, b){return 0.5 - Math.random()});
  questions.splice(game_length, questions.length)
}
// Activates when the user clicks submit. Checks the answer they put in against the correct answer and provides feedback. If correct they gain a point and are told it is correct. If incorrect they are told the correct answer. 
function submit(){
  input = questions[i].selection
  lower = input.toLowerCase()
  answering = false

  if (questions[i].type == 'word') {
    if (lower.includes(questions[i].answer)){
    questions[i].result = 'Correct'
    points += 1
    } else {
    questions[i].result = "Wrong. The correct answer was '" + questions[i].answer + "'."
    }
  } else {
    if (questions[i].selection === questions[i].answer){
    questions[i].result = 'Correct'
    points += 1
    } else {
    questions[i].result = "Wrong. The correct answer was '" + questions[i].answer + "'."
    }
  } 
}
// Brings up the next question, if the user has finished all the questions it adds their score, name, and age to the leaderboard. 
function next(){
  i += 1
  answering = true
  if (i === questions.length){
    leaderboard.splice(leaderboard.length, 0, {name:name, age:age, points:points})
  }
}
// Resets the player name and age, but doesn't change the questions.
function reset(){
  i = 0
  points = 0
  answering = true
  named = false
  name = ""
  age = 0
  error_message = ''
  for (let r = 0; r < questions.length; r++) {
        questions[r].selection = ""
        questions[r].result = ""
  }
}
// Play again function. The player stays the same and the questions are changed.
function again(){
  shuffle() 
  i = 0
  points = 0
  answering = true
  named = true
}
// This runs when the submit button is clicked at the start. Checks if the name and age are valid inputs, returns an error message if they are not, otherwise the quiz starts. Shuffles if it is the first time through, otherwise assumes that multiple players are playing and does not shuffle the quiz.
function begin(){
  error_message = ''
  if (age > 118 || age <= 0){
    age = 0
    error_message += ' Please enter a realistic age.'
  } 
  if (name == ''){
    error_message += ' Enter your name.'
  } 
  if (age <= 118 && age > 0 && name != '') {
    named = true
  }
  if (first_time){
    shuffle()
  }
  first_time = false
}
// Allows users to press enter rather than clicking the button
document.addEventListener('keyup', (event) => {
  if (event.keyCode === 13){
    if (named === false){
      begin()
    } else if (i >= questions.length){
      again()
    }else if (answering === true){
      submit()
    } else if (answering === false){
      next()
    } 
  }
});

</script>

<h1>Riddles</h1>
{#if named}
  {#if (i < questions.length)}
  {questions[i].question} {questions[i].number}
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
      <input type="number" bind:value={questions[i].selection}> {questions[i].selection}
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
    Well done {name}, you got {points} / {questions.length}!
    <button on:click={reset}>
      New player
    </button>

    <button on:click={again}>
      Play again
    </button>

    <br>
    Leaderboard:
    <br>

    <table>
      <tr>
        <th>
          Name
        </th>
        <th>
          Age
        </th>
        <th>
          Score
        </th>
      </tr>
      {#each leaderboard as score}
      <tr>
        <th>
          {score.name}
        </th>
        <th>
          {score.age}
        </th>
        <th>
          {score.points} / {questions.length}
        </th>
      </tr>
      {/each}
    </table>
    
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
  <br>
  {error_message}
{/if}


<style>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  table, tr, th {
    border: black
     solid 2px;
  }
</style>

