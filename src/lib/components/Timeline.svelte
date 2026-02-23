<!--
@component
Timeline.svelte — Chronological timeline list

Displays events in chronological order with dates and descriptions.

USAGE EXAMPLE:
<Timeline
  title="Program Timeline"
  events={[
    { date: '2006-01-01', description: 'School founded.' },
    { date: '2025-08-01', description: 'Scholarship milestone reached.' }
  ]}
/>
-->
<script>
  let {
    title = 'Timeline',
    events = [],
  } = $props();

  function toTimestamp(dateString) {
    const date = new Date(dateString);
    return Number.isNaN(date.getTime()) ? 0 : date.getTime();
  }

  function formatDate(dateString) {
    const date = new Date(dateString);

    if (Number.isNaN(date.getTime())) {
      return dateString;
    }

    return new Intl.DateTimeFormat('en-US', {
      year: 'numeric',
      month: 'short',
      day: 'numeric',
    }).format(date);
  }

  function getSortedEvents() {
    return [...events].sort((a, b) => toTimestamp(a.date) - toTimestamp(b.date));
  }
</script>

{#if events.length > 0}
  <aside class="timeline" aria-labelledby="timeline-title">
    <h2 id="timeline-title" class="timeline-title">{title}</h2>

    <ol class="timeline-list">
      {#each getSortedEvents() as event}
        <li class="timeline-item">
          <time class="timeline-date" datetime={event.date}>{formatDate(event.date)}</time>
          <p class="timeline-description">{event.description}</p>
        </li>
      {/each}
    </ol>
  </aside>
{/if}

<style lang="scss">
  @use '../styles' as *;

  .timeline {
    margin-top: var(--spacing-xl);
    margin-bottom: var(--spacing-xl); 
    padding: 0 var(--spacing-md) var(--spacing-md);
    border: var(--border-width-thin) solid var(--color-border);
    background-color: var(--color-light-gray);
  }

  .timeline-title {
    margin: 0;
    padding-top: 0;
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    line-height: 1.2;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--color-dark);
  }

  .timeline-list {
    list-style: none;
    margin: var(--spacing-md) 0 0;
    padding: 0;
    border-left: var(--border-width-thin) solid var(--color-border);
  }

  .timeline-item {
    position: relative;
    margin-left: var(--spacing-sm);
    padding: 0 0 var(--spacing-md) var(--spacing-md);

    &:last-child {
      padding-bottom: 0;
    }

    &::before {
      content: '';
      position: absolute;
      top: 0.35rem;
      left: calc(-1 * var(--spacing-sm));
      width: 0.5rem;
      height: 0.5rem;
      border-radius: 50%;
      background-color: var(--color-accent);
      transform: translateX(-50%);
    }
  }

  .timeline-date {
    display: inline-block;
    margin-bottom: var(--spacing-xs);
    font-family: var(--font-sans);
    font-size: var(--font-size-xs);
    font-weight: 700;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: var(--color-accent);
  }

  .timeline-description {
    margin: 0;
    font-family: var(--font-sans);
    font-size: var(--font-size-base);
    color: var(--color-text);
    line-height: 1.6;
  }
</style>