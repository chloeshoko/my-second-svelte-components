<!--
@component
ContextBox.svelte — Story context summary box

Displays brief background bullets and an optional source link.

USAGE EXAMPLE:
<ContextBox
  title="Why This Matters"
  items={[
    'Bullet one',
    'Bullet two'
  ]}
  sourceLabel="Read the full report"
  sourceHref="https://example.com/report"
/>
-->
<script>
  let {
    title = 'Why This Matters',
    items = [],
    sourceLabel = '',
    sourceHref = '',
  } = $props();
</script>

{#if items.length > 0}
  <aside class="context-box" aria-labelledby="context-box-title">
    <h2 id="context-box-title" class="context-box-title">{title}</h2>

    <ul class="context-box-list">
      {#each items as item}
        <li class="context-box-item">{item}</li>
      {/each}
    </ul>

    {#if sourceLabel && sourceHref}
      <a class="context-box-source" href={sourceHref}>{sourceLabel}</a>
    {/if}
  </aside>
{/if}

<style lang="scss">
  @use '../styles' as *;

  .context-box {
    margin: var(--spacing-lg) 0;
    padding: 1px var(--spacing-md) var(--spacing-sm);
    border-left: var(--border-width-accent) solid var(--color-accent);
    background-color: var(--color-light-gray);
  }

  .context-box-title {
    margin: var(--spacing-xs) 0 var(--spacing-xs);
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--color-dark);
  }

  .context-box-list {
    margin: 0;
    padding-left: var(--spacing-md);
  }

  .context-box-item {
    margin-bottom: var(--spacing-xs);
    font-family: var(--font-sans);
    font-size: var(--font-size-base);
    color: var(--color-text);
    line-height: 1.6;

    &:last-child {
      margin-bottom: 0;
    }
  }

  .context-box-source {
    display: inline-block;
    margin-top: var(--spacing-sm);
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
</style>