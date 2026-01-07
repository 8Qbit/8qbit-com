<script>
  import PurpleTentacle from './PurpleTentacle.svelte';
  
  let { name, title, tagline, summary } = $props();
</script>

<header class="header">
  <div class="header-content">
    <div class="avatar-section">
      <div class="avatar-frame">
        <PurpleTentacle size={120} />
      </div>
    </div>
    
    <div class="info-section">
      <h1 class="name">{name}</h1>
      <p class="title">{title}</p>
      <p class="tagline">"{tagline}"</p>
    </div>
  </div>
  
  <div class="summary-box">
    <span class="prompt">&gt; ABOUT.EXE</span>
    <p class="summary">{summary}</p>
  </div>
</header>

<style>
  .header {
    text-align: center;
    padding: calc(var(--pixel-size) * 8) calc(var(--pixel-size) * 4);
    margin-bottom: calc(var(--pixel-size) * 4);
    background: linear-gradient(
      180deg,
      transparent 0%,
      rgba(123, 45, 142, 0.1) 50%,
      transparent 100%
    );
  }
  
  .header-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: calc(var(--pixel-size) * 4);
  }
  
  @media (min-width: 600px) {
    .header-content {
      flex-direction: row;
      justify-content: center;
      gap: calc(var(--pixel-size) * 8);
    }
  }
  
  .avatar-section {
    flex-shrink: 0;
  }
  
  .avatar-frame {
    display: inline-block;
    position: relative;
    padding: 12px;
  }
  
  .info-section {
    text-align: center;
  }
  
  @media (min-width: 600px) {
    .info-section {
      text-align: left;
    }
  }
  
  .name {
    font-family: 'Press Start 2P', cursive;
    font-size: 1.5rem;
    color: var(--text-light);
    text-shadow: 
      calc(var(--pixel-size)) calc(var(--pixel-size)) 0 var(--tentacle-purple-dark),
      calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 rgba(0,0,0,0.5);
    margin-bottom: calc(var(--pixel-size) * 3);
    line-height: 1.4;
  }
  
  .title {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.8rem;
    color: var(--green-glow);
    text-shadow: calc(var(--pixel-size)) calc(var(--pixel-size)) 0 rgba(0,0,0,0.5);
    margin-bottom: calc(var(--pixel-size) * 2);
  }
  
  .tagline {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.55rem;
    color: var(--orange-light);
    font-style: italic;
  }
  
  .summary-box {
    margin-top: calc(var(--pixel-size) * 6);
    background: rgba(0, 0, 0, 0.4);
    border: calc(var(--pixel-size)) solid var(--tentacle-purple);
    padding: calc(var(--pixel-size) * 4);
    text-align: left;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
  }
  
  .prompt {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.6rem;
    color: var(--green-glow);
    display: block;
    margin-bottom: calc(var(--pixel-size) * 2);
  }
  
  .summary {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.55rem;
    color: var(--text-light);
    line-height: 2.2;
    opacity: 0.9;
  }
</style>
