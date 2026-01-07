<script>
  import PixelCard from './PixelCard.svelte';
  
  let { education = [] } = $props();
</script>

<PixelCard title="Education">
  <div class="education-list">
    {#each education as edu, index}
      <article class="edu-item" style="--delay: {index * 0.15}s">
        <div class="edu-icon">
          <svg viewBox="0 0 24 24" width="32" height="32" aria-hidden="true">
            <!-- Pixel art graduation cap -->
            <rect x="2" y="12" width="20" height="2" fill="var(--tentacle-purple)" />
            <rect x="4" y="10" width="16" height="2" fill="var(--tentacle-purple)" />
            <rect x="6" y="14" width="12" height="6" fill="var(--tentacle-purple-dark)" />
            <rect x="10" y="8" width="4" height="4" fill="var(--orange-warm)" />
            <rect x="11" y="6" width="2" height="2" fill="var(--orange-warm)" />
          </svg>
        </div>
        <div class="edu-content">
          <h3 class="degree">{edu.degree}</h3>
          <p class="institution">{edu.institution}</p>
          <div class="edu-meta">
            <span class="period">{edu.period}</span>
            <span class="focus">{edu.focus}</span>
          </div>
        </div>
      </article>
    {/each}
  </div>
</PixelCard>

<style>
  .education-list {
    display: flex;
    flex-direction: column;
    gap: calc(var(--pixel-size) * 5);
  }
  
  .edu-item {
    display: flex;
    gap: calc(var(--pixel-size) * 4);
    align-items: flex-start;
    padding: calc(var(--pixel-size) * 3);
    background: rgba(123, 45, 142, 0.05);
    border-left: calc(var(--pixel-size) * 2) solid var(--tentacle-purple);
    animation: fade-in 0.4s ease-out forwards;
    animation-delay: var(--delay);
    opacity: 0;
  }
  
  @keyframes fade-in {
    to {
      opacity: 1;
    }
  }
  
  .edu-icon {
    flex-shrink: 0;
    animation: pixel-bounce 2s steps(4) infinite;
  }
  
  @keyframes pixel-bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-4px); }
  }
  
  .edu-icon svg {
    image-rendering: pixelated;
  }
  
  .edu-content {
    flex: 1;
  }
  
  .degree {
    font-size: 0.65rem;
    color: var(--tentacle-purple);
    margin-bottom: calc(var(--pixel-size) * 1);
  }
  
  .institution {
    font-size: 0.55rem;
    color: var(--orange-warm);
    margin-bottom: calc(var(--pixel-size) * 2);
  }
  
  .edu-meta {
    display: flex;
    flex-wrap: wrap;
    gap: calc(var(--pixel-size) * 3);
    font-size: 0.5rem;
  }
  
  .period {
    color: var(--green-slime);
  }
  
  .focus {
    color: var(--text-muted);
  }
  
  .focus::before {
    content: '// ';
    color: var(--blue-electric);
  }
</style>
