<script lang='ts'>
  import PtsCanvas from "$lib/ptscanvas/PtsCanvas.svelte";
  import type {CanvasForm, CanvasSpace } from "pts";

  function handleAnimate( space:CanvasSpace, form: CanvasForm, time?:number, ftime?:number) {
    form.point( space.pointer, 10) ;
  }

  function handleAction( space:CanvasSpace, form:CanvasForm, type:string, px:number, py:number) {
    if (type==='click') {
      console.log( type, px, py );
    }
  }
</script>


<div class="container">
<PtsCanvas setup={{bgcolor: '#f0f'}} onAnimate={handleAnimate} onAction={handleAction} ></PtsCanvas>
</div>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>


<style>
  .container {
    width: 500px;
    height: 500px;
  }
</style>