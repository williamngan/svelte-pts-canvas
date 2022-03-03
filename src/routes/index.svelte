<script>
  import PtsCanvas from "$lib/index.svelte";

  function handleAnimate( space, form, time, ftime) {
    form.point( space.pointer, 10) ;
  }

  function handleAction( space, form, type, px, py) {
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