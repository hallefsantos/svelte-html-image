<script context="module">
   let canvasEl;
   let phraseBg;

   export const generateCanvas = (phrase) => {   
      const ctx = canvasEl.getContext("2d");
      const maxWidth = 400;
      const primary = phrase.portuguese;
      const secondary = phrase.portuguese_en;
      const x = (canvasEl.width - maxWidth) / 2;

      ctx.drawImage(phraseBg, 0, 0);
      ctx.font = "36px Helvetica";
      ctx.fillStyle = '#111';

      wrapText(ctx, primary, x, 220, maxWidth, 45);
      
      ctx.font = "26px Helvetica";
      ctx.fillStyle = '#111';

      wrapText(ctx, secondary, x, (270 +(36*getLines(ctx, primary, (maxWidth - 100)).length)), maxWidth, 35);
      generateLink();
   }

   const generateLink = () => {
      if(window.navigator.msSaveBlob) {
         window.navigator.msSaveBlob(canvasEl.msToBlob(), "phrase-image.png")
      } else {
         const a = document.createElement('a');
         document.body.appendChild(a);
         a.href = canvasEl.toDataURL();
         a.download = 'phrase-image.png';
         a.click();
         document.body.removeChild(a);
      }
   }

   function wrapText(context, text, x, y, maxWidth, lineHeight) {
      const words = text.split(' ');
      let line = '';

      for (let n = 0; n < words.length; n++) {
         const testLine = line + words[n] + ' ';
         const metrics = context.measureText(testLine);
         const testWidth = metrics.width;
         if (testWidth > maxWidth && n > 0) {
            context.fillText(line, x, y);
            line = words[n] + ' ';
            y += lineHeight;
         } else {
            line = testLine;
         }
      }
      context.fillText(line, x, y);
   }

   function getLines(ctx, text, maxWidth) {
      var words = text.split(" ");
      var lines = [];
      var currentLine = words[0];

      for (var i = 1; i < words.length; i++) {
         var word = words[i];
         var width = ctx.measureText(currentLine + " " + word).width;
         console.log(maxWidth);
         if (width < maxWidth) {
            currentLine += " " + word;
         } else {
            lines.push(currentLine);
            currentLine = word;
         }
      }
      lines.push(currentLine);
      return lines;
   }
</script>

<canvas bind:this={canvasEl}  class="hidden" width="600" height="600"></canvas>
<img bind:this={phraseBg} class="hidden" src="frase.jpg">