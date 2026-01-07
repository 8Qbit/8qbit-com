<script>
  let { title = '', children } = $props();
</script>

<section class="pixel-card">
  {#if title}
    <h2 class="section-header">{title}</h2>
  {/if}
  <div class="card-content">
    {@render children()}
  </div>
</section>

<style>
  .pixel-card {
    background: var(--dialog-bg);
    color: var(--text-dark);
    padding: calc(var(--pixel-size) * 6);
    margin: calc(var(--pixel-size) * 6) 0;
    position: relative;
    
    /* Chunky pixel border effect */
    border: calc(var(--pixel-size) * 2) solid var(--dialog-border);
    
    /* Inner highlight and shadow for depth */
    box-shadow: 
      inset calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 rgba(255,255,255,0.5),
      inset calc(var(--pixel-size) * -2) calc(var(--pixel-size) * -2) 0 rgba(0,0,0,0.1),
      calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 rgba(0,0,0,0.4);
    
    transition: transform 0.1s steps(2), box-shadow 0.1s steps(2);
  }
  
  .pixel-card:hover {
    transform: translate(calc(var(--pixel-size) * -1), calc(var(--pixel-size) * -1));
    box-shadow: 
      inset calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 rgba(255,255,255,0.5),
      inset calc(var(--pixel-size) * -2) calc(var(--pixel-size) * -2) 0 rgba(0,0,0,0.1),
      calc(var(--pixel-size) * 3) calc(var(--pixel-size) * 3) 0 rgba(0,0,0,0.4);
  }
  
  .section-header {
    display: inline-block;
    background: var(--tentacle-purple);
    color: var(--text-light);
    padding: calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 4);
    margin-bottom: calc(var(--pixel-size) * 4);
    border: calc(var(--pixel-size)) solid var(--tentacle-purple-dark);
    box-shadow: 
      calc(var(--pixel-size)) calc(var(--pixel-size)) 0 var(--tentacle-purple-dark);
    font-family: 'Press Start 2P', cursive;
    font-size: 0.75rem;
    text-transform: uppercase;
  }
  
  .card-content {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.65rem;
    line-height: 2;
  }
</style>
