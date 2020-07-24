<script>
   import Card from './Card.svelte';
   import GenerateImage, { generateCanvas } from './GenerateImage.svelte';

   let generateImagePhrase = '';

   const phrases = [
      {
         portuguese: 'A esperança é a última que morre.', 
         portuguese_en: "While there's life, there's hope."
      },
      {
         portuguese: 'A união faz a força.', 
         portuguese_en: "Many hands make light work."
      },
      {
         portuguese: 'Quando um não quer, dois não brigam.', 
         portuguese_en: "It takes two to tango."
      },
      {
         portuguese: 'Vivendo e aprendendo.', 
         portuguese_en: "You live and learn."
      },
      {
         portuguese: 'Saco vazio não para em pé.', 
         portuguese_en: "An empty bag won't stand."
      },
      {
         portuguese: 'Rir é o melhor remédio.', 
         portuguese_en: "Laughter is the best medicine."
      },
   ];

   let generateState = false;

   const clicou = frase => {
      console.log(frase);
      generateImagePhrase = frase;
      generateCanvas();
      generateState = true;
   }

</script>

<section class="div flex flex-wrap align-top py-20">
   {#each phrases as phrase}
      <Card on:click={() => clicou(phrase) } {phrase} />
   {/each}

   <GenerateImage state={generateState}  phrase={generateImagePhrase} />
</section>
<style>
   
</style>