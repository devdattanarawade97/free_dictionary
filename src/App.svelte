

<script>

  let word='';
  $:quoteUrl=`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`;
  
  let responseMeaning='';
  

async  function getMeaning(e){
  e.preventDefault();

    const response=await fetch(quoteUrl);
    const responseJson=await response.json();

     const meanings=responseJson[0].meanings[0].definitions[0].definition
     responseMeaning=meanings;
    // console.log(responseMeaning);
   
  }
 
</script>
<style>
  @import 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css';

  h1{
    color: purple;
   
  }
  

  button{
    background-color: purple;
    border-radius: 5px;
    color: white;
  }
  h2{

    color: purple;
  }


  #input-key{
    width: 700px;
  }

  @media(max-width:700px){

   #input-key{
    width: auto;
   }
  }
</style>



<div class="row">
  <div class="col">

    <h1 class="display-5 fw-bold text-center" >
      Free Dictionary
    </h1>
  
    <div class="">
     
      <input type="text" class=" mt-5 mb-3 p-2 " bind:value={word} id="input-key" placeholder="search meaning">
    <button class="mt-3" on:click={getMeaning}>submit</button>
     
    
  
    </div>
  
    <div class="">
      {#if responseMeaning!==''}
      
      {#await responseMeaning}
        <h2>Loading...</h2>
      {:then responseMeaning} 
          
      <h2 class="mt-5" >Meaning : {responseMeaning}</h2>
      {/await}
      {/if}
    </div>
  </div>
</div>

