<script context="module">
   let canvasEl;
   let phraseBg;

   export const generateCanvas = (phrase) => {   
      const ctx = canvasEl.getContext("2d");
      const maxWidth = 690;
      const primary = phrase.portuguese;
      const secondary = phrase.portuguese_en;
      const x = (canvasEl.width - maxWidth) / 2;

      ctx.drawImage(phraseBg, 0, 0);
      ctx.font = "75px Helvetica";
      ctx.fillStyle = '#111';

      wrapText(ctx, primary, x, 380, maxWidth, 80);
      
      ctx.font = "48px Helvetica";
      ctx.fillStyle = '#111';

      wrapText(ctx, secondary, x, (400 +(75*getLines(ctx, primary, 420).length)), maxWidth, 65);
      // generateLink();

      console.log(getLines(ctx, primary, 420));
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

<canvas bind:this={canvasEl} width="1080" height="1080"></canvas>
<img bind:this={phraseBg} class="hidden" src="frase.jpg">