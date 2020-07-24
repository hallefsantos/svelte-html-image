<script>
   export let phrase;
   import GenerateImage from './GenerateImage.svelte';
</script>

<style>
   article span {
      transition: .2s;
   }
</style>

<article class="lg:w-1/3 md:w-1/2 w-full px-2 mb-5">
   <div class="shadow mr-2 p-3 h-full">
      <div class="flex">
         <h2 class="font-bold text-xl flex-1"> 
            {phrase.portuguese}
         </h2>
         <span on:click class="w-8 h-8 bg-gray-300 hover:bg-gray-400 rounded-full flex items-center justify-center">
            <svg class="w-6 h-6 cursor-pointer hover:color-green-400" width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg" data-svg="download"><polyline fill="none" stroke="#000" points="14,10 9.5,14.5 5,10"></polyline><rect x="3" y="17" width="13" height="1"></rect><line fill="none" stroke="#000" x1="9.5" y1="13.91" x2="9.5" y2="3"></line></svg>
         </span>
      </div>
      <p class="italic mt-2 text-gray-600 text-lg">{phrase.portuguese_en}</p>
   </div>
</article>