<script>
  import PixelCard from './PixelCard.svelte';
  
  let { contact = {} } = $props();
  
  const contactItems = [
    { key: 'email', icon: 'M', label: 'Email', prefix: 'mailto:' },
    { key: 'linkedin', icon: 'in', label: 'LinkedIn', prefix: 'https://' },
    { key: 'github', icon: '<>', label: 'GitHub', prefix: 'https://' },
    { key: 'website', icon: 'W', label: 'Website', prefix: 'https://' }
  ];
</script>

<PixelCard title="Contact">
  <div class="contact-grid">
    {#each contactItems as item, index}
      {#if contact[item.key]}
        <a 
          href="{item.prefix}{contact[item.key]}" 
          class="contact-item"
          target={item.key !== 'email' ? '_blank' : undefined}
          rel={item.key !== 'email' ? 'noopener noreferrer' : undefined}
          style="--delay: {index * 0.1}s"
        >
          <div class="contact-header">
            <span class="contact-icon">{item.icon}</span>
            <span class="contact-label">{item.label}</span>
          </div>
          <span class="contact-value">{contact[item.key]}</span>
        </a>
      {/if}
    {/each}
  </div>
  
  <div class="cta-section">
    <p class="cta-text">Ready to take over the world together?</p>
    <a href="mailto:{contact.email}" class="pixel-button">
      Send Message
    </a>
  </div>
</PixelCard>

<style>
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: calc(var(--pixel-size) * 3);
    margin-bottom: calc(var(--pixel-size) * 6);
  }
  
  .contact-item {
    display: flex;
    flex-direction: column;
    gap: calc(var(--pixel-size) * 2);
    padding: calc(var(--pixel-size) * 3);
    background: rgba(123, 45, 142, 0.05);
    border: calc(var(--pixel-size)) solid transparent;
    text-decoration: none;
    color: var(--text-dark);
    transition: all 0.1s steps(2);
    animation: fade-slide 0.3s ease-out forwards;
    animation-delay: var(--delay);
    opacity: 0;
    transform: translateX(-10px);
  }
  
  @keyframes fade-slide {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }
  
  .contact-item:hover {
    background: rgba(123, 45, 142, 0.1);
    border-color: var(--tentacle-purple);
    transform: translateX(4px);
  }
  
  .contact-header {
    display: flex;
    align-items: center;
    gap: calc(var(--pixel-size) * 2);
  }
  
  .contact-icon {
    width: calc(var(--pixel-size) * 8);
    height: calc(var(--pixel-size) * 8);
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--tentacle-purple);
    color: var(--text-light);
    font-size: 0.5rem;
    font-weight: bold;
    border: calc(var(--pixel-size)) solid var(--tentacle-purple-dark);
    box-shadow: calc(var(--pixel-size)) calc(var(--pixel-size)) 0 rgba(0,0,0,0.3);
    flex-shrink: 0;
  }
  
  .contact-label {
    font-size: 0.6rem;
    color: var(--text-light);
    text-transform: uppercase;
    font-weight: bold;
  }
  
  .contact-value {
    font-size: 0.5rem;
    color: var(--blue-electric);
    word-break: break-all;
    padding-left: calc(var(--pixel-size) * 10);
  }
  
  .cta-section {
    text-align: center;
    padding-top: calc(var(--pixel-size) * 4);
    border-top: calc(var(--pixel-size)) dashed var(--dialog-border-light);
  }
  
  .cta-text {
    font-size: 0.6rem;
    color: var(--tentacle-purple);
    margin-bottom: calc(var(--pixel-size) * 4);
  }
  
  .pixel-button {
    display: inline-block;
    background: var(--tentacle-purple);
    color: var(--text-light);
    padding: calc(var(--pixel-size) * 3) calc(var(--pixel-size) * 6);
    font-family: 'Press Start 2P', cursive;
    font-size: 0.6rem;
    text-decoration: none;
    border: calc(var(--pixel-size) * 2) solid var(--tentacle-purple-dark);
    box-shadow: 
      inset calc(var(--pixel-size) * -2) calc(var(--pixel-size) * -2) 0 var(--tentacle-purple-dark),
      inset calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 var(--tentacle-purple-light),
      calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 rgba(0,0,0,0.4);
    cursor: pointer;
    transition: all 0.1s steps(2);
  }
  
  .pixel-button:hover {
    transform: translate(calc(var(--pixel-size) * -1), calc(var(--pixel-size) * -1));
    box-shadow: 
      inset calc(var(--pixel-size) * -2) calc(var(--pixel-size) * -2) 0 var(--tentacle-purple-dark),
      inset calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 var(--tentacle-purple-light),
      calc(var(--pixel-size) * 3) calc(var(--pixel-size) * 3) 0 rgba(0,0,0,0.4);
    background: var(--tentacle-purple-light);
  }
  
  .pixel-button:active {
    transform: translate(calc(var(--pixel-size)), calc(var(--pixel-size)));
    box-shadow: 
      inset calc(var(--pixel-size) * -2) calc(var(--pixel-size) * -2) 0 var(--tentacle-purple-dark),
      inset calc(var(--pixel-size) * 2) calc(var(--pixel-size) * 2) 0 var(--tentacle-purple-light),
      0 0 0 rgba(0,0,0,0.4);
  }
</style>
