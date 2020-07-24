<script context="module">
   import html2canvas from 'html2canvas';
   let phraseEl;
   export const generateCanvas = () => {
      setTimeout(() => {
         html2canvas(phraseEl).then(function(canvas) {

            if(window.navigator.msSaveBlob) {
               window.navigator.msSaveBlob(canvas.msToBlob(), "phrase-image.png")
            } else {
               const a = document.createElement('a');
               document.body.appendChild(a);
               a.href = canvas.toDataURL();
               a.download = 'phrase-image.png';
               a.click();
               document.body.removeChild(a);
            }
         });
      }, 100);
   }
</script>

<script>
   export let phrase = '';
   export let state = false;
</script>

<style>
   .frase {
      width: 600px;
      height: 600px;
      opacity: 1;
   }
</style>

<div bind:this="{phraseEl}" class="{state ? 'block' : 'hidden' } border border-gray-300 p-5 frase flex items-center justify-center flex-col relative">
   <img class="absolute inset-0" src="frase.jpg" alt="">
   <div class="relative z-10 max-w-sm text-gray-800">
      <h2 class="text-4xl mb-5">{phrase.portuguese}</h2>
      <p class="text-2xl">{phrase.portuguese_en}</p>
   </div>
</div>