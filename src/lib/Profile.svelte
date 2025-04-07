<script lang="ts">
  // Add default export for the component
  export {};

  const profile = {
    name: "Oliver Seidl",
    title: "Software Engineer",
    avatar: "https://api.dicebear.com/7.x/pixel-art/svg?seed=John&backgroundColor=0D1117",
    bio: "15 Year Old Student at ______ based in Prague, Czech Republic"
  };

  interface Link {
    title: string;
    url: string;
  }

  interface Category {
    name: string;
    links: Link[];
  }

  const categories: Category[] = [
    {
      name: "Cybersecurity",
      links: [
        {
          title: "TryHackMe",
          url: "https://tryhackme.com/p/olinkkt"
        }
      ]
    },
    {
      name: "Software Development",
      links: [
        {
          title: "GitHub",
          url: "https://github.com/olinkkt"
        },
        {
          title: "CodeWars",
          url: "https://www.codewars.com/users/olinkkt"
        },
        {
          title: "Exercism",
          url: "https://exercism.org/profiles/olinkkt"
        }
      ]
    }
  ];
</script>

<section class="profile-container">
  <div class="terminal">
    <div class="terminal-header">
      <span class="controls">
        <span class="control close"></span>
        <span class="control minimize"></span>
        <span class="control maximize"></span>
      </span>
      <span class="title">oliver@dev:~/portfolio</span>
    </div>
    <div class="terminal-content">
      <!-- Profile Section -->
      <div class="profile-section">
        <div class="avatar-container">
          <img 
            src={profile.avatar} 
            alt="Profile avatar" 
            class="avatar"
          />
        </div>
        
        <div class="info">
          <pre class="code-comment">// Hello, World! ud83dudc4b</pre>
          <h1>{profile.name}</h1>
          <h2><span class="keyword">const</span> role = <span class="string">"{profile.title}"</span>;</h2>
          <p class="comment">/**</p>
          <p class="comment"> * {profile.bio}</p>
          <p class="comment"> */</p>
        </div>
      </div>

      <!-- Command Line Separator -->
      <div class="command-line">
        <span class="prompt">oliver@dev</span>:<span class="path">~/portfolio</span>$ <span class="command">cat links.json | jq</span>
      </div>

      <!-- Links Section -->
      <div class="links-section">
        <div class="json-view">
          <span class="json-brace">&#123;</span>
          {#each categories as category, i}
            <div class="category" style="--delay: {i * 0.1}s">
              <div class="json-key-container">
                <span class="json-key">"{category.name}"</span><span class="json-colon">:</span> <span class="json-brace">[</span>
              </div>
              <div class="link-group">
                {#each category.links as link, j (link.title)}
                  <a 
                    href={link.url}
                    target="_blank"
                    rel="noopener noreferrer"
                    class="link-card"
                    style="--item-delay: {j * 0.1}s"
                  >
                    <div class="link-content">
                      <span class="json-brace">&#123;</span>
                      <div class="link-json-content">
                        <div><span class="json-key">"name"</span><span class="json-colon">:</span> <span class="json-string">"{link.title}"</span>,</div>
                        <div class="link-url"><span class="json-key">"url"</span><span class="json-colon">:</span> <span class="json-string">"{link.url}"</span></div>
                      </div>
                      <span class="json-brace">&#125;</span>
                    </div>
                    <div class="link-hover">
                      <span class="code-function">open</span>(<span class="code-string">"{link.title}"</span>);
                    </div>
                  </a>
                  {#if j !== category.links.length - 1}
                    <div class="json-comma">,</div>
                  {/if}
                {/each}
              </div>
              <div class="json-brace-end">]</div>
              {#if i !== categories.length - 1}
                <div class="json-comma">,</div>
              {/if}
            </div>
          {/each}
          <span class="json-brace">&#125;</span>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .profile-container {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
    padding: 2rem 0;
    animation: fadeIn 0.8s ease-out;
  }

  .terminal {
    background: var(--surface);
    border-radius: 8px;
    overflow: hidden;
    box-shadow: var(--card-shadow);
    border: 1px solid rgba(97, 218, 251, 0.1);
  }

  .terminal-header {
    background: var(--surface-lighter);
    padding: 0.5rem 1rem;
    display: flex;
    align-items: center;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .controls {
    display: flex;
    gap: 0.5rem;
  }

  .control {
    width: 12px;
    height: 12px;
    border-radius: 50%;
  }

  .close { background: #ff5f56; }
  .minimize { background: #ffbd2e; }
  .maximize { background: #27c93f; }

  .terminal-header .title {
    margin-left: 1rem;
    color: var(--secondary);
    font-size: 0.9rem;
    font-family: 'JetBrains Mono', monospace;
  }

  .terminal-content {
    padding: 1.5rem;
    font-family: 'JetBrains Mono', monospace;
  }

  /* Profile Section Styles */
  .profile-section {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
    border-bottom: 1px dashed rgba(255, 255, 255, 0.1);
    padding-bottom: 1.5rem;
  }

  .avatar-container {
    display: flex;
    align-items: flex-start;
  }

  .avatar {
    width: 120px;
    height: 120px;
    border-radius: 8px;
    object-fit: cover;
    border: 1px solid rgba(97, 218, 251, 0.2);
    transition: transform 0.3s ease;
  }

  .avatar:hover {
    transform: scale(1.02);
  }

  .info {
    position: relative;
  }

  .code-comment {
    color: #6A9955;
    font-size: 1rem;
    margin-bottom: 1rem;
    font-family: 'JetBrains Mono', monospace;
  }

  h1 {
    font-size: 2.5rem;
    color: var(--accent);
    margin-bottom: 0.5rem;
    font-weight: 700;
  }

  h2 {
    font-size: 1.25rem;
    color: var(--primary);
    margin-bottom: 1.5rem;
    font-weight: 400;
  }

  .keyword {
    color: #569CD6;
  }

  .string {
    color: #CE9178;
  }

  .comment {
    color: #6A9955;
    font-size: 1rem;
    line-height: 1.6;
  }

  /* Command Line Styles */
  .command-line {
    display: flex;
    align-items: center;
    margin: 1rem 0;
    font-size: 0.9rem;
  }

  .prompt {
    color: #27c93f;
    font-weight: 500;
  }

  .path {
    color: #61dafb;
    font-weight: 500;
  }

  .command {
    color: var(--primary);
    margin-left: 0.5rem;
  }

  /* Links Section Styles */
  .links-section {
    margin-top: 1rem;
  }

  .json-view {
    position: relative;
    padding: 0.5rem;
  }

  .category {
    margin-left: 1.5rem;
    margin-bottom: 1rem;
    opacity: 0;
    transform: translateY(10px);
    animation: slideIn 0.5s ease-out forwards;
    animation-delay: var(--delay);
  }

  .json-key-container {
    margin-bottom: 0.5rem;
  }

  .json-key {
    color: #9CDCFE;
  }

  .json-string {
    color: #CE9178;
  }

  .json-colon {
    color: var(--primary);
    margin: 0 0.25rem;
  }

  .json-brace {
    color: #D4D4D4;
  }

  .json-brace-end {
    margin-left: 1rem;
    color: #D4D4D4;
  }

  .json-comma {
    color: #D4D4D4;
    margin-left: 1rem;
    margin-bottom: 0.5rem;
  }

  .link-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-left: 2rem;
  }

  .link-card {
    padding: 0.75rem;
    background-color: var(--surface);
    border: 1px solid rgba(97, 218, 251, 0.05);
    border-radius: 4px;
    text-decoration: none;
    color: var(--primary);
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    opacity: 0;
    transform: translateX(-10px);
    animation: slideInRight 0.5s ease-out forwards;
    animation-delay: calc(var(--delay) + var(--item-delay));
    position: relative;
    overflow: hidden;
  }

  .link-card:hover {
    transform: translateY(-2px);
    border-color: var(--accent);
    background: var(--surface-lighter);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .link-content {
    transition: transform 0.3s ease;
  }

  .link-json-content {
    margin-left: 1rem;
    margin-top: 0.25rem;
    margin-bottom: 0.25rem;
  }

  .link-url {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 100%;
  }

  .link-hover {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--surface-lighter);
    opacity: 0;
    transform: translateY(100%);
    transition: all 0.3s ease;
  }

  .link-card:hover .link-hover {
    opacity: 1;
    transform: translateY(0);
  }

  .link-card:hover .link-content {
    transform: translateY(-100%);
  }

  .code-function {
    color: #DCDCAA;
  }

  .code-string {
    color: #CE9178;
  }

  .cursor {
    display: inline-block;
    width: 8px;
    height: 16px;
    background-color: var(--accent);
    animation: blink 1s step-end infinite;
    vertical-align: middle;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes slideIn {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes slideInRight {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  @media (max-width: 768px) {
    .profile-container {
      padding: 1rem;
    }

    h1 {
      font-size: 2rem;
    }

    h2 {
      font-size: 1.1rem;
    }

    .avatar {
      width: 100px;
      height: 100px;
    }

    .command-line {
      font-size: 0.8rem;
      flex-wrap: wrap;
    }

    .link-json-content {
      font-size: 0.8rem;
    }
  }
</style>