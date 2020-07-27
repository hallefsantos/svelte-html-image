<script>
   import Card from './Card.svelte';
   import GenerateImage, { generateCanvas } from './GenerateImage.svelte';

   const phrases = [
      {
         portuguese: 'De grão em grão a galinha enche o papo.', 
         portuguese_en: "Little by little the bird builds its nest."
      },
      {
         portuguese: 'A união faz a força.', 
         portuguese_en: "Many hands make light work."
      },
      {
         portuguese: 'A grama da vizinho é sempre mais verde.', 
         portuguese_en: "The grass is always greener on the other side of the fence."
      },
      {
         portuguese: 'Não deixe para amanhã o que você pode fazer agora.', 
         portuguese_en: "Never put off till tomorrow what you can do today."
      },
      {
         portuguese: 'Água mole em pedra dura tanto bate até que fura.', 
         portuguese_en: "Water dropping day by day wears the hardest rock away."
      },
      {
         portuguese: 'Cada um por si e Deus por todos. Cada um por si e Deus por todos', 
         portuguese_en: "Every man for himself (and the devil take the hindmost) (and the devil take the hindmost)."
      },
   ];

   let generateState = false;

   const clicou = frase => {
      generateCanvas(frase);
   }

</script>

<section class="div flex flex-wrap align-top py-10">
   {#each phrases as phrase}
      <Card on:click={() => clicou(phrase) } {phrase} />
   {/each}
</section>

<GenerateImage />