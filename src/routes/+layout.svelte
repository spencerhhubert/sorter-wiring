<script>
  import '../app.css';
  import { page } from '$app/stores';

  let { children } = $props();
  let path = $derived($page.url.pathname);
</script>

<div class="wrap">
  <nav class="top">
    <span class="brand">Sorter V2 wiring</span>
    <a href="/" class:active={path === '/'}>Wire harness</a>
    <a href="/steppers" class:active={path === '/steppers'}>Stepper connectors</a>
    <a href="/setup" class:active={path === '/setup'}>Setup photos</a>
  </nav>
  {@render children()}
</div>
