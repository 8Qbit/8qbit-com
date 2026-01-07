<script>
  import './lib/styles/pixel-art.css';
  import cvData from './lib/data/cv.json';
  import qbitData from './lib/data/8qbit.json';
  import PurpleTentacle from './lib/components/PurpleTentacle.svelte';
  
  // Profile state: '8qbit' (default) or 'professional'
  let activeProfile = $state('8qbit');
  let isProfileFlipping = $state(false);
  
  // Current data based on profile
  let currentData = $derived(activeProfile === '8qbit' ? qbitData : cvData);
  
  let activeSection = $state('look');
  let isChangingChannel = $state(false);
  
  const sections = [
    { id: 'look', label: 'Look at' },
    { id: 'experience', label: 'Experience' },
    { id: 'skills', label: 'Skills' },
    { id: 'education', label: 'Education' },
    { id: 'talk', label: 'Talk to' }
  ];
  
  function setSection(id) {
    if (id === activeSection) return;
    
    // Trigger channel change animation
    isChangingChannel = true;
    
    // Change section after brief delay
    setTimeout(() => {
      activeSection = id;
    }, 150);
    
    // Remove animation class after it completes
    setTimeout(() => {
      isChangingChannel = false;
    }, 400);
  }
  
  function handleProfileFlip() {
    // Start flip animations
    isProfileFlipping = true;
    
    // Toggle profile after brief delay (when content is hidden by flip)
    setTimeout(() => {
      activeProfile = activeProfile === '8qbit' ? 'professional' : '8qbit';
    }, 200);
    
    // Remove flip animation class
    setTimeout(() => {
      isProfileFlipping = false;
    }, 500);
  }
  
  // Apply theme class to body
  $effect(() => {
    document.body.classList.remove('theme-8qbit', 'theme-professional');
    document.body.classList.add(activeProfile === '8qbit' ? 'theme-8qbit' : 'theme-professional');
  });
</script>

<div class="game-screen">
  <!-- TV Effects - Subtle bad reception -->
  <div class="tv-vignette"></div>
  <div class="tv-rolling"></div>
  <div class="tv-flicker"></div>
  <div class="tv-ghosting"></div>
  <div class="tv-wobble"></div>
  
  <!-- Channel Change Overlay -->
  <div class="channel-change-overlay" class:active={isChangingChannel}>
    <div class="channel-bar"></div>
  </div>
  
  <!-- Main Scene Area -->
  <div class="scene-area">
    <!-- Header/Character Display -->
    <header class="character-header">
      <div class="portrait-frame">
        <PurpleTentacle 
          size={120} 
          isFlipped={activeProfile === 'professional'}
          onFlip={handleProfileFlip}
        />
      </div>
      <div class="character-info" class:profile-flipping={isProfileFlipping}>
        <h1 class="pixel-title">{currentData.name}</h1>
        <p class="pixel-subtitle">{currentData.title}</p>
        <p class="tagline">"{currentData.tagline}"</p>
      </div>
    </header>

    <!-- SCUMM-style Verb Bar - Now under header -->
    <nav class="verb-bar" class:profile-flipping-delay-1={isProfileFlipping}>
      {#each sections as section}
        <button 
          class="verb-btn" 
          class:active={activeSection === section.id}
          onclick={() => setSection(section.id)}
        >
          {section.label}
        </button>
      {/each}
    </nav>

    <!-- Content Area based on active section -->
    <main class="content-area" class:profile-flipping-delay-2={isProfileFlipping}>
      {#if activeSection === 'look'}
        <div class="dialog-box">
          <h2 class="dialog-title">* About {activeProfile === '8qbit' ? '8Qbit' : 'Me'} *</h2>
          <p class="dialog-text">{currentData.summary}</p>
        </div>
      {/if}
      
      {#if activeSection === 'experience'}
        <div class="dialog-box">
          <h2 class="dialog-title">* {activeProfile === '8qbit' ? 'Adventures' : 'Work Experience'} *</h2>
          <div class="experience-list">
            {#each currentData.experience as job}
              <article class="experience-item">
                <div class="job-header">
                  <h3 class="job-title">{job.role}</h3>
                  <span class="job-period">{job.period}</span>
                </div>
                <p class="job-company">{job.company} - {job.location}</p>
                <ul class="job-highlights">
                  {#each job.highlights as highlight}
                    <li>{highlight}</li>
                  {/each}
                </ul>
              </article>
            {/each}
          </div>
        </div>
      {/if}
      
      {#if activeSection === 'skills'}
        <div class="dialog-box">
          <h2 class="dialog-title">* {activeProfile === '8qbit' ? 'Inventory' : 'Skills'} *</h2>
          <div class="skills-container">
            {#each Object.entries(currentData.skills) as [category, skillList], i}
              <div class="skill-category">
                <h3 class="category-label">{category}</h3>
                <div class="skill-list">
                  {#each skillList as skill}
                    <span class="skill-tag" class:purple={i % 3 === 0} class:orange={i % 3 === 1}>
                      {skill}
                    </span>
                  {/each}
                </div>
              </div>
            {/each}
          </div>
        </div>
      {/if}
      
      {#if activeSection === 'education'}
        <div class="dialog-box">
          <h2 class="dialog-title">* {activeProfile === '8qbit' ? 'Learning Log' : 'Education'} *</h2>
          <div class="education-list">
            {#each currentData.education as edu}
              <article class="education-item">
                <h3 class="edu-degree">{edu.degree}</h3>
                <p class="edu-school">{edu.institution}</p>
                <p class="edu-meta">{edu.period} • {edu.focus}</p>
              </article>
            {/each}
          </div>
        </div>
      {/if}
      
      {#if activeSection === 'talk'}
        <div class="dialog-box">
          <h2 class="dialog-title">* Talk to {activeProfile === '8qbit' ? '8Qbit' : 'Paul'} *</h2>
          <div class="contact-options">
            <p class="dialog-text">Select a topic:</p>
            <div class="contact-grid">
              {#if activeProfile === 'professional'}
                <!-- Professional: Email, LinkedIn, GitHub, Discord -->
                <a href="mailto:{currentData.contact.email}" class="contact-option">
                  <span class="contact-icon">
                    <svg viewBox="0 0 24 24" fill="currentColor">
                      <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
                    </svg>
                  </span>
                  <span class="contact-label">Email</span>
                </a>
                <a href="https://{currentData.contact.linkedin}" target="_blank" rel="noopener" class="contact-option">
                  <span class="contact-icon">
                    <svg viewBox="0 0 24 24" fill="currentColor">
                      <path d="M19 3a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h14m-.5 15.5v-5.3a3.26 3.26 0 0 0-3.26-3.26c-.85 0-1.84.52-2.32 1.3v-1.11h-2.79v8.37h2.79v-4.93c0-.77.62-1.4 1.39-1.4a1.4 1.4 0 0 1 1.4 1.4v4.93h2.79M6.88 8.56a1.68 1.68 0 0 0 1.68-1.68c0-.93-.75-1.69-1.68-1.69a1.69 1.69 0 0 0-1.69 1.69c0 .93.76 1.68 1.69 1.68m1.39 9.94v-8.37H5.5v8.37h2.77z"/>
                    </svg>
                  </span>
                  <span class="contact-label">LinkedIn</span>
                </a>
              {/if}
              
              <!-- Both profiles: GitHub -->
              <a href="https://{currentData.contact.github}" target="_blank" rel="noopener" class="contact-option">
                <span class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2A10 10 0 0 0 2 12c0 4.42 2.87 8.17 6.84 9.5.5.08.66-.23.66-.5v-1.69c-2.77.6-3.36-1.34-3.36-1.34-.46-1.16-1.11-1.47-1.11-1.47-.91-.62.07-.6.07-.6 1 .07 1.53 1.03 1.53 1.03.87 1.52 2.34 1.07 2.91.83.09-.65.35-1.09.63-1.34-2.22-.25-4.55-1.11-4.55-4.92 0-1.11.38-2 1.03-2.71-.1-.25-.45-1.29.1-2.64 0 0 .84-.27 2.75 1.02.79-.22 1.65-.33 2.5-.33.85 0 1.71.11 2.5.33 1.91-1.29 2.75-1.02 2.75-1.02.55 1.35.2 2.39.1 2.64.65.71 1.03 1.6 1.03 2.71 0 3.82-2.34 4.66-4.57 4.91.36.31.69.92.69 1.85V21c0 .27.16.59.67.5C19.14 20.16 22 16.42 22 12A10 10 0 0 0 12 2z"/>
                  </svg>
                </span>
                <span class="contact-label">GitHub</span>
              </a>
              
              <!-- Both profiles: Discord -->
              <a href="https://discord.com/users/{currentData.contact.discord || '8qbit_'}" target="_blank" rel="noopener" class="contact-option">
                <span class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="currentColor">
                    <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057 19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028 14.09 14.09 0 0 0 1.226-1.994.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/>
                  </svg>
                </span>
                <span class="contact-label">Discord</span>
              </a>
            </div>
          </div>
        </div>
      {/if}
    </main>
  </div>
  
  <!-- Status Bar -->
  <footer class="status-bar">
    <span class="profile-indicator">{activeProfile === '8qbit' ? '8Qbit' : 'Paul Nylund'}</span>
    <span class="cursor-blink">{activeSection === 'look' ? 'Look at' : activeSection === 'talk' ? 'Talk to' : activeSection.charAt(0).toUpperCase() + activeSection.slice(1)} {activeProfile === '8qbit' ? '8Qbit' : 'Paul'}</span>
  </footer>
</div>

<style>
  /* Character Header */
  .character-header {
    display: flex;
    align-items: center;
    gap: calc(var(--pixel) * 6);
    padding: calc(var(--pixel) * 4);
    flex-wrap: wrap;
    justify-content: center;
  }
  
  @media (min-width: 600px) {
    .character-header {
      justify-content: flex-start;
    }
  }
  
  .portrait-frame {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  
  .character-info {
    text-align: center;
  }
  
  @media (min-width: 600px) {
    .character-info {
      text-align: left;
    }
  }
  
  .tagline {
    font-size: 0.6rem;
    color: var(--mansion-accent);
    margin-top: calc(var(--pixel) * 2);
    font-style: italic;
  }
  
  /* Verb Bar - Now positioned under header, framed like dialog box */
  .verb-bar {
    background: var(--scumm-bg);
    border: var(--pixel) solid var(--scumm-border);
    padding: calc(var(--pixel) * 3);
    display: flex;
    flex-wrap: wrap;
    gap: calc(var(--pixel) * 2);
    justify-content: center;
    margin: calc(var(--pixel) * 2) calc(var(--pixel) * 4);
    position: relative;
    transition: border-color 0.4s ease, background-color 0.4s ease;
  }
  
  .verb-bar::before {
    content: '';
    position: absolute;
    top: calc(var(--pixel) * -1);
    left: calc(var(--pixel) * -1);
    right: calc(var(--pixel) * -1);
    bottom: calc(var(--pixel) * -1);
    border: calc(var(--pixel) / 2) solid var(--scumm-highlight);
    pointer-events: none;
    transition: border-color 0.4s ease;
  }
  
  /* Content Area */
  .content-area {
    flex: 1;
    overflow-y: auto;
    padding-bottom: calc(var(--pixel) * 4);
  }
  
  /* Experience List - No timeline bar */
  .experience-list {
    display: flex;
    flex-direction: column;
    gap: calc(var(--pixel) * 5);
  }
  
  .experience-item {
    padding-bottom: calc(var(--pixel) * 4);
    border-bottom: calc(var(--pixel) / 2) dashed var(--scumm-border);
  }
  
  .experience-item:last-child {
    border-bottom: none;
    padding-bottom: 0;
  }
  
  /* Job/Experience Styles */
  .job-header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: baseline;
    gap: calc(var(--pixel) * 2);
    margin-bottom: calc(var(--pixel) * 2);
  }
  
  .job-title {
    font-size: 0.75rem;
    color: var(--text-gold);
  }
  
  .job-period {
    font-size: 0.55rem;
    color: var(--green-light);
    background: var(--green-dark);
    padding: calc(var(--pixel)) calc(var(--pixel) * 2);
    border: calc(var(--pixel) / 2) solid var(--green-main);
  }
  
  .job-company {
    font-size: 0.6rem;
    color: var(--purple-light);
    margin-bottom: calc(var(--pixel) * 2);
  }
  
  .job-highlights {
    list-style: none;
    padding: 0;
  }
  
  .job-highlights li {
    font-size: 0.55rem;
    color: var(--text-cream);
    padding: calc(var(--pixel)) 0;
    padding-left: calc(var(--pixel) * 4);
    position: relative;
    line-height: 1.8;
  }
  
  .job-highlights li::before {
    content: '>';
    position: absolute;
    left: 0;
    color: var(--text-cyan);
  }
  
  /* Education List - No timeline bar */
  .education-list {
    display: flex;
    flex-direction: column;
    gap: calc(var(--pixel) * 5);
  }
  
  .education-item {
    padding-bottom: calc(var(--pixel) * 4);
    border-bottom: calc(var(--pixel) / 2) dashed var(--scumm-border);
  }
  
  .education-item:last-child {
    border-bottom: none;
    padding-bottom: 0;
  }
  
  /* Skills Container */
  .skills-container {
    display: grid;
    gap: calc(var(--pixel) * 4);
  }
  
  .skill-category {
    border-bottom: calc(var(--pixel) / 2) dashed var(--scumm-border);
    padding-bottom: calc(var(--pixel) * 3);
  }
  
  .skill-category:last-child {
    border-bottom: none;
  }
  
  .category-label {
    font-size: 0.6rem;
    color: var(--text-cyan);
    text-transform: uppercase;
    margin-bottom: calc(var(--pixel) * 2);
  }
  
  .skill-list {
    display: flex;
    flex-wrap: wrap;
    gap: calc(var(--pixel));
  }
  
  /* Education Styles */
  .edu-degree {
    font-size: 0.7rem;
    color: var(--text-gold);
    margin-bottom: calc(var(--pixel));
  }
  
  .edu-school {
    font-size: 0.6rem;
    color: var(--purple-light);
    margin-bottom: calc(var(--pixel));
  }
  
  .edu-meta {
    font-size: 0.55rem;
    color: var(--text-cream);
    opacity: 0.8;
  }
  
  /* Contact Styles */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: calc(var(--pixel) * 3);
    margin-top: calc(var(--pixel) * 4);
  }
  
  .contact-option {
    display: flex;
    align-items: center;
    gap: calc(var(--pixel) * 2);
    padding: calc(var(--pixel) * 3) calc(var(--pixel) * 4);
    background: var(--scumm-button);
    border: calc(var(--pixel) / 2) solid var(--scumm-border);
    text-decoration: none;
    transition: all 0.15s;
  }
  
  .contact-option:hover {
    background: var(--scumm-highlight);
    transform: translateX(calc(var(--pixel) * 2));
  }
  
  .contact-option:hover .contact-icon,
  .contact-option:hover .contact-label {
    color: var(--scumm-bg);
  }
  
  .contact-icon {
    width: calc(var(--pixel) * 8);
    height: calc(var(--pixel) * 8);
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--purple-main);
    color: var(--text-white);
    flex-shrink: 0;
    padding: calc(var(--pixel) * 1.5);
  }
  
  .contact-icon svg {
    width: 100%;
    height: 100%;
  }
  
  .contact-label {
    font-size: 0.55rem;
    color: var(--text-gold);
    display: block;
  }
  
  /* Status Bar Profile Indicator */
  .profile-indicator {
    color: var(--text-cyan);
    margin-right: calc(var(--pixel) * 4);
  }
  
  .status-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }


</style>
