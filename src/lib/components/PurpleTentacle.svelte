<script>
  // Purple Tentacle / Profile flip card
  // Click to flip between Purple Tentacle (8Qbit) and real photo (Professional)
  
  let { size = 120, isFlipped = false, onFlip = () => {} } = $props();
  
  function handleClick(event) {
    event.stopPropagation();
    onFlip();
  }
  
  function handleKeydown(event) {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      onFlip();
    }
  }
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div 
  class="profile-frame" 
  class:flipped={isFlipped}
  style="--size: {size}px"
>
  <!-- Clickable flip card -->
  <button 
    type="button"
    class="flip-card"
    onclick={handleClick}
    onkeydown={handleKeydown}
    aria-label="Click to switch between 8Qbit and Professional profile"
  >
    <div class="flip-card-inner">
      <!-- Front - Purple Tentacle (8Qbit profile) -->
      <div class="flip-card-front">
        <img 
          src="/images/purple-tentacle.png" 
          alt="Purple Tentacle - 8Qbit profile"
          class="profile-image"
        />
      </div>
      
      <!-- Back - Real Photo (Professional profile) -->
      <div class="flip-card-back">
        <img 
          src="/images/paul.jpg" 
          alt="Paul Nylund - Professional profile"
          class="profile-image"
        />
      </div>
    </div>
  </button>
</div>

<style>
  .profile-frame {
    --pixel: 3px;
    width: var(--size);
    height: var(--size);
    position: relative;
    perspective: 1000px;
    animation: invite-shake 3s ease-in-out infinite;
    animation-delay: 2s;
    
    /* Match dialog-box styling - no padding, image fills to border */
    background: var(--scumm-bg, #000033);
    border: var(--pixel) solid var(--scumm-border, #6666AA);
  }
  
  /* Outer highlight like dialog-box::before */
  .profile-frame::before {
    content: '';
    position: absolute;
    top: calc(var(--pixel) * -1);
    left: calc(var(--pixel) * -1);
    right: calc(var(--pixel) * -1);
    bottom: calc(var(--pixel) * -1);
    border: calc(var(--pixel) / 2) solid var(--scumm-highlight, #AAAAFF);
    pointer-events: none;
  }
  
  /* Subtle shake animation to invite clicking */
  @keyframes invite-shake {
    0%, 100% {
      transform: rotate(0deg);
    }
    2% {
      transform: rotate(-2deg);
    }
    4% {
      transform: rotate(2deg);
    }
    6% {
      transform: rotate(-2deg);
    }
    8% {
      transform: rotate(2deg);
    }
    10% {
      transform: rotate(0deg);
    }
  }
  
  /* Stop shaking on hover - user noticed it */
  .profile-frame:hover {
    animation: none;
  }
  
  /* The flip card button */
  .flip-card {
    width: 100%;
    height: 100%;
    position: relative;
    cursor: pointer;
    background: transparent;
    border: none;
    padding: 0;
    outline: none;
  }
  
  .flip-card:focus-visible {
    outline: 2px solid #FFD700;
    outline-offset: 8px;
  }
  
  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 0.6s ease-in-out;
    transform-style: preserve-3d;
  }
  
  .profile-frame.flipped .flip-card-inner {
    transform: rotateY(180deg);
  }
  
  .flip-card-front,
  .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    overflow: hidden;
  }
  
  .flip-card-back {
    transform: rotateY(180deg);
  }
  
  .profile-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    image-rendering: auto;
    display: block;
  }
  
  .flip-card-front .profile-image {
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    object-fit: cover;
  }
</style>
