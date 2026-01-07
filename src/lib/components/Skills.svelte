<script>
  import PixelCard from './PixelCard.svelte';
  
  let { skills = {} } = $props();
  
  // Map skill categories to colors
  const categoryColors = {
    languages: '',
    frontend: 'orange',
    backend: 'blue',
    cloud: '',
    databases: 'orange',
    tools: 'blue'
  };
  
  const categoryLabels = {
    languages: 'Languages',
    frontend: 'Frontend',
    backend: 'Backend',
    cloud: 'Cloud & DevOps',
    databases: 'Databases',
    tools: 'Tools'
  };
</script>

<PixelCard title="Skills">
  <div class="skills-grid">
    {#each Object.entries(skills) as [category, skillList], catIndex}
      <div class="skill-category" style="--cat-delay: {catIndex * 0.1}s">
        <h3 class="category-title">{categoryLabels[category] || category}</h3>
        <div class="skill-tags">
          {#each skillList as skill, skillIndex}
            <span 
              class="pixel-tag" 
              class:orange={categoryColors[category] === 'orange'}
              class:blue={categoryColors[category] === 'blue'}
              style="--skill-delay: {skillIndex * 0.05}s"
            >
              {skill}
            </span>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</PixelCard>

<style>
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: calc(var(--pixel-size) * 5);
  }
  
  .skill-category {
    animation: slide-up 0.3s ease-out forwards;
    animation-delay: var(--cat-delay);
    opacity: 0;
    transform: translateY(10px);
  }
  
  @keyframes slide-up {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .category-title {
    font-size: 0.55rem;
    color: var(--tentacle-purple);
    margin-bottom: calc(var(--pixel-size) * 2);
    padding-bottom: calc(var(--pixel-size));
    border-bottom: calc(var(--pixel-size)) solid var(--tentacle-purple);
    display: inline-block;
  }
  
  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: calc(var(--pixel-size) * 2);
  }
  
  .pixel-tag {
    display: inline-block;
    background: var(--green-slime);
    color: var(--text-light);
    padding: calc(var(--pixel-size)) calc(var(--pixel-size) * 2);
    font-size: 0.45rem;
    border: calc(var(--pixel-size)) solid #2E7D32;
    box-shadow: calc(var(--pixel-size)) calc(var(--pixel-size)) 0 rgba(0,0,0,0.3);
    transition: transform 0.1s steps(2), background 0.1s steps(2);
    cursor: default;
    animation: pop-in 0.2s ease-out forwards;
    animation-delay: calc(var(--cat-delay) + var(--skill-delay));
    opacity: 0;
    transform: scale(0.8);
  }
  
  @keyframes pop-in {
    to {
      opacity: 1;
      transform: scale(1);
    }
  }
  
  .pixel-tag:hover {
    transform: scale(1.1) translateY(-2px);
    background: var(--green-glow);
  }
  
  .pixel-tag.orange {
    background: var(--orange-warm);
    border-color: #D35400;
  }
  
  .pixel-tag.orange:hover {
    background: var(--orange-light);
  }
  
  .pixel-tag.blue {
    background: var(--blue-electric);
    border-color: #2980B9;
  }
  
  .pixel-tag.blue:hover {
    background: var(--blue-light);
  }
</style>
