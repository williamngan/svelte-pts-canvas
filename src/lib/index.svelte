<script lang="ts">

  import { onMount, onDestroy } from "svelte";
  import { Bound, CanvasForm, CanvasSpace } from "pts";
  import type {CanvasSpaceOptions, IPlayer} from "pts";

  export let name:string = '';
  export let style:any = {};
  export let play:boolean = true;
  export let touch:boolean = true;
  export let setup:CanvasSpaceOptions = {bgcolor: '#9ab', retina: true, resize: true};
  
  export let onStart: (bound: Bound, space:CanvasSpace, form:CanvasForm) => void = undefined;
  export let onAnimate: (space:CanvasSpace, form:CanvasForm, time?: number, ftime?: number) => void = undefined;
  export let onResize: (space:CanvasSpace, form:CanvasForm, size?: Bound, evt?: Event) => void = undefined;
  export let onAction: (space:CanvasSpace, form:CanvasForm, type: string, px: number, py: number, evt?:Event) => void = undefined;
  
  let space: CanvasSpace;
  let initialPlay: boolean = true;

  onMount(() => {
    space = new CanvasSpace(`__pts__${name}`).setup(setup);
    let form = space.getForm();
    
    // if (player) player(space, form);
    const player:IPlayer = {
      start: onStart ? ( b, s ) => onStart(b, space, form) : undefined,
      animate: onAnimate ? (time, ftime) => onAnimate(space, form, time, ftime) : undefined,
      action: onAction ? (type, px, py, evt) => onAction( space, form, type, px, py, evt) : undefined,
      resize: onResize ? (bound, evt) => onResize( space, form, bound, evt) : undefined,
    };

    if (onAnimate) {
      space.add( player );
    }

    if (touch) space.bindMouse().bindTouch();
    if (play) space.play();
    
    initialPlay = play;
  });

  onDestroy(() => {
    if (space) {
      space.removeAll();
      space.stop();
    }
  });

  $: {
    if (space) {
      if (play) {
        if (initialPlay) {
          space.resume();
        } else {
          space.play();
        }
      } else {
        space.pause(true);
      }
    }
  }
</script>

<div id="__pts__{name}" class="__pts" {style} />

<style>
  .__pts {
    width: 100%;
    height: 100%;
  }
</style>