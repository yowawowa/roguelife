<script lang="ts">
  let isRunning = $state(false);
  const startRun = (): void => {
    console.log("Run started");
    isRunning = true;
  };

  let selectedQuest = $state<Quest | null>(null);
  const selectQuest = (quest: Quest): void => {
    selectedQuest = quest;
  };

  type Quest = {
    title: string;
    duration: number;
  };

  const quests: Quest[] = [
    { title: "Read a book", duration: 20 },
    { title: "Learn GO", duration: 30 },
    { title: "Walk the dog", duration: 15 },
  ];
</script>

<main class="container">
  {#if !isRunning}
    <h1 class="title">
      <span class="title-accent">Roguelife</span>
    </h1>
    <p class="subtitle">A roguelike approach to everyday tasks</p>

    <div class="start">
      <button aria-label="start-btn" class="btn" onclick={startRun}
        >START RUN
      </button>
    </div>
  {:else}
    {#if !selectedQuest}
      <div class="quest-list">
        {#each quests as quest}
          <button class="quest-card" onclick={() => selectQuest(quest)}>
            <h2>{quest.title}</h2>
            <p>{quest.duration} min</p>
          </button>
        {/each}
      </div>
    {:else}
      <div class="quest-card">
        <h2>{selectedQuest.title}</h2>
        <p>{selectedQuest.duration} min</p>
      </div>
    {/if}
  {/if}
</main>

<style>
  :global(html),
  :global(body) {
    margin: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  :global(body) {
    background: #141821;
    color: #e5e7eb;
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100%;
    padding: 20px;
    box-sizing: border-box;
  }

  .quest-list {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
  }
  .quest-list {
    display: flex;
    justify-content: center;
    gap: 20px;
  }

  .quest-card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 180px;
    height: 240px;
    padding: 20px;
    background: #252525;
    border: 1px solid #555;
    border-radius: 8px;
    box-sizing: border-box;
  }

  .quest-card h2 {
    font-size: 20px;
  }

  .quest-card p {
    font-size: 14px;
    color: #aaa;
  }
  .quest-card {
    cursor: pointer;
    transition:
      border-color 0.2s,
      transform 0.2s;
  }

  .quest-card:hover {
    border-color: #a78bfa;
    transform: translateY(-5px);
  }
</style>
