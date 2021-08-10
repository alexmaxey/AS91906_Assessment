<script>
  let i = 0
    let questions = [
    {question:"",
    type:"multi",
    a1:"",
    v1:"",
    a2:"",
    v2:"",
    a3:"",
    v3:"",
    a4:"",
    v4:"", 
    selection:"",
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

function next(){
  i += 1
}
</script>

<h1>Riddles</h1>

<button on:click={next}>
  Submit
</button>

{#each questions as queries}
{queries.question}
<br>
<label>
  <input type="radio" bind:group={queries.selection} value={queries.v1}>
  {queries.a1}
</label>
<label>
  <input type="radio" bind:group={queries.selection} value={queries.v2}>
  {queries.a2}
</label>
<label>
  <input type="radio" bind:group={queries.selection} value={queries.v3}>
  {queries.a3}
</label>
<label>
  <input type="radio" bind:group={queries.selection} value={queries.v4}>
  {queries.a4}
</label>
<br>
{queries.result}
<br>
{/each}

