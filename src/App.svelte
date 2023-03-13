<script lang="ts">
  import { onMount } from "svelte";

  let canvas: HTMLCanvasElement;
  let w: number;
  let h: number;

  const squareDimension = 100;

  let x = 0;
  let y = 0;

  let xIncrement = 1;

  onMount(() => {
    canvas.width = w;
    canvas.height = h;

    const ctx = canvas.getContext("2d");
    let animationFrame = requestAnimationFrame(loop);

    function loop() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();
      ctx.rect(x, y, squareDimension, squareDimension);
      ctx.fill();

      if (x + squareDimension > w || x < 0) {
        xIncrement *= -1;
      }
      // x += xIncrement;

      animationFrame = requestAnimationFrame(loop);
    }
  });
</script>

<div bind:clientWidth={w} bind:clientHeight={h}>
  <canvas bind:this={canvas} width={200} height={200} />
</div>

<style>
  div {
    height: 100vh;
  }
  canvas {
  }
</style>
