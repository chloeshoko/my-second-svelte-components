<!--
@component
AuthorBio.svelte — Compact author profile box

Displays an author photo, name, title, and social links.

USAGE EXAMPLE:
<AuthorBio
  photoSrc="/example-photo.gif"
  photoAlt="Portrait of Jane Smith"
  name="Jane Smith"
  title="Staff Reporter"
  socialLinks={[
    { label: 'X', href: 'https://x.com/' },
    { label: 'LinkedIn', href: 'https://www.linkedin.com/' }
  ]}
/>
-->
<script>
  let {
    photoSrc,
    photoAlt = '',
    name,
    title = '',
    socialLinks = [],
  } = $props();
</script>

<aside class="author-bio" aria-label="Author bio">
  <img class="author-photo" src={photoSrc} alt={photoAlt} />

  <div class="author-content">
    <h2 class="author-name">{name}</h2>

    {#if title}
      <p class="author-title">{title}</p>
    {/if}

    {#if socialLinks.length > 0}
      <ul class="author-social-list" aria-label="Author social links">
        {#each socialLinks as link}
          <li>
            <a class="author-social-link" href={link.href}>{link.label}</a>
          </li>
        {/each}
      </ul>
    {/if}
  </div>
</aside>

<style lang="scss">
  @use '../styles' as *;

  .author-bio {
    display: grid;
    grid-template-columns: 80px 1fr;
    gap: var(--spacing-sm);
    align-items: center;
    margin-top: var(--spacing-xl);
    padding: var(--spacing-sm);
    border: var(--border-width-thin) solid var(--color-border);
    background-color: var(--color-light-gray);
  }

  .author-photo {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    object-fit: cover;
  }

  .author-name {
    margin: 0;
    font-family: var(--font-serif);
    font-size: var(--font-size-lg);
    font-weight: 700;
    color: var(--color-dark);
  }

  .author-title {
    margin: var(--spacing-xs) 0 0;
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    color: var(--color-medium-gray);
    text-transform: uppercase;
    letter-spacing: 0.02em;
  }

  .author-social-list {
    display: flex;
    flex-wrap: wrap;
    gap: var(--spacing-sm);
    list-style: none;
    margin: var(--spacing-xs) 0 0;
    padding: 0;
  }

  .author-social-link {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    color: var(--color-accent);
    text-decoration: none;

    &:hover {
      color: var(--color-accent-hover);
      text-decoration: underline;
    }
  }

  @include mobile {
    .author-bio {
      grid-template-columns: 1fr;
      text-align: center;
      justify-items: center;
    }

    .author-social-list {
      justify-content: center;
    }
  }
</style>