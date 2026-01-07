<script>
  import PixelCard from './PixelCard.svelte';
  
  let { experience = [] } = $props();
</script>

<PixelCard title="Work Experience">
  <div class="experience-list">
    {#each experience as job, index}
      <article class="job" style="--delay: {index * 0.1}s">
        <div class="job-header">
          <h3 class="role">{job.role}</h3>
          <span class="period">{job.period}</span>
        </div>
        <div class="company-info">
          <span class="company">{job.company}</span>
          <span class="location">@ {job.location}</span>
        </div>
        <ul class="highlights">
          {#each job.highlights as highlight}
            <li>{highlight}</li>
          {/each}
        </ul>
      </article>
    {/each}
  </div>
</PixelCard>

<style>
  .experience-list {
    display: flex;
    flex-direction: column;
    gap: calc(var(--pixel-size) * 6);
  }
  
  .job {
    padding-bottom: calc(var(--pixel-size) * 4);
    border-bottom: calc(var(--pixel-size)) dashed var(--dialog-border-light);
    animation: slide-in 0.3s ease-out forwards;
    animation-delay: var(--delay);
    opacity: 0;
    transform: translateX(-10px);
  }
  
  .job:last-child {
    border-bottom: none;
    padding-bottom: 0;
  }
  
  @keyframes slide-in {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }
  
  .job-header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: baseline;
    gap: calc(var(--pixel-size) * 2);
    margin-bottom: calc(var(--pixel-size) * 2);
  }
  
  .role {
    font-size: 0.7rem;
    color: var(--tentacle-purple);
    text-shadow: calc(var(--pixel-size)) calc(var(--pixel-size)) 0 rgba(123, 45, 142, 0.2);
  }
  
  .period {
    font-size: 0.5rem;
    color: var(--green-slime);
    background: rgba(76, 175, 80, 0.1);
    padding: calc(var(--pixel-size)) calc(var(--pixel-size) * 2);
    border: calc(var(--pixel-size)) solid var(--green-slime);
  }
  
  .company-info {
    display: flex;
    flex-wrap: wrap;
    gap: calc(var(--pixel-size) * 2);
    margin-bottom: calc(var(--pixel-size) * 3);
  }
  
  .company {
    font-size: 0.6rem;
    color: var(--orange-warm);
  }
  
  .location {
    font-size: 0.5rem;
    color: var(--text-muted);
  }
  
  .highlights {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .highlights li {
    font-size: 0.55rem;
    line-height: 2.2;
    padding-left: calc(var(--pixel-size) * 4);
    position: relative;
    color: var(--text-dark);
    opacity: 0.85;
  }
  
  .highlights li::before {
    content: '>';
    position: absolute;
    left: 0;
    color: var(--tentacle-purple);
    font-weight: bold;
  }
  
  .highlights li:hover {
    opacity: 1;
    color: var(--tentacle-purple-dark);
  }
</style>
