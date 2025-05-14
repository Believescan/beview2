<script>
  import '../styles/global.css';
</script>

<svelte:head>
  <title>BeView | Believe Token Dashboard</title>
</svelte:head>

<div class="app-container">
  <nav class="sidebar">
  </nav>
  
  <main class="main-content">
    <slot />
  </main>
</div>