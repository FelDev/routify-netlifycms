<script>
  import { TabsTransition } from "@roxi/routify/decorators";
  import { writable } from "svelte/store";
  import BottomNav from "./_components/BottomNav.svelte";
  import { url, isActive } from "@roxi/routify";
  
  const width = writable();
  const color = writable();
  const _urls = [
    ["./homepage", "🏠", "#FF6500"],
    ["./markdown", "markdown", "#8FD5DB"],
    ["./team", "Team", "#88F0d0"],
  ];
  $: urls = _urls.map(([path, name, color]) => ({
    name,
    href: $url(path),
    color,
    active: !!$isActive(path)
  }));

</script>

<style>
  :global(body) {
    padding: 0;
  }
  * :global(.inset) {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  div.inset {
    bottom: 64px;
    overflow: hidden;
  }

</style>
<div style="height: 100%">

  <div class="inset" bind:offsetWidth={$width}>
    <slot decorator={TabsTransition} scoped={{ width }} />
  </div>
  <BottomNav {urls} height="64px" />
</div>
