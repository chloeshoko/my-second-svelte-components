<!--
@component
KeyTakeaways.svelte — Highlighted key takeaways box

Displays a title and bullet list inside a highlighted container.

USAGE EXAMPLE:
<KeyTakeaways
  title="Key Takeaways"
  items={[
    'Point one',
    'Point two',
    'Point three'
  ]}
/>
-->
<script>
  let {
    title = 'Key Takeaways',
    items = [],
  } = $props();
</script>

{#if items.length > 0}
  <aside class="takeaways" aria-labelledby="takeaways-title">
    <h2 id="takeaways-title" class="takeaways-title">{title}</h2>
    <ul class="takeaways-list">
      {#each items as item}
        <li class="takeaways-item">{item}</li>
      {/each}
    </ul>
  </aside>
{/if}

<style lang="scss">
  @use '../styles' as *;

  .takeaways {
    margin-top: var(--spacing-xl);
    padding: var(--spacing-md);
    border-left: var(--border-width-accent) solid var(--color-accent);
    background-color: var(--color-light-gray);
  }

  .takeaways-title {
    margin: 0 0 var(--spacing-sm);
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    color: var(--color-dark);
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .takeaways-list {
    margin: 0;
    padding-left: var(--spacing-md);
  }

  .takeaways-item {
    margin-bottom: var(--spacing-xs);
    font-family: var(--font-sans);
    font-size: var(--font-size-base);
    color: var(--color-text);
    line-height: 1.6;

    &:last-child {
      margin-bottom: 0;
    }
  }
</style>