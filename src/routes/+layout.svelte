<script lang="ts">
  import { ModeWatcher } from 'mode-watcher';
  import '../app.css';
  import ThemeSwitcher from '$lib/components/ThemeSwitcher.svelte';
  let { children } = $props();
</script>

<ModeWatcher />
<ThemeSwitcher />
{@render children()}
