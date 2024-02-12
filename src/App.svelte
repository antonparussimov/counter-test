<script>
  import Unit from "./lib/Unit.svelte";

  let counters = [
    { title: 'new', count: 0 }
  ];

  function addCounter() {
    counters = [...counters, { title: 'new', count: 0 }];
  }

  /**
     * @param {number} index
     */
  function removeCounter(index) {
    counters = counters.filter((_, id) => id !== index);
  }

  /**
     * @param {number} index
     */
  function increment(index) {
    counters[index].count += 1;
  }

  /**
     * @param {number} index
     */
  function decrement(index) {
    if (counters[index].count > 0) {
      counters[index].count -= 1;
    }
  }

  /**
     * @param {number} index
     * @param {string} text
     */
  function changeTitle(index, text) {
    counters[index].title = text;
  }
</script>

<div class="text-center">
  <h1 class="text-[4rem]">Multiple Counter</h1>
  {#each counters as { title, count }, index (index)}
    <Unit 
      {title} 
      {count} 
      on:remove={() => removeCounter(index)}
      on:increment={() => increment(index)}
      on:decrement={() => decrement(index)}
      on:changeTitle={(e) => changeTitle(index, e.detail.text)}
    />
  {/each}
  <button class="text-center max-w-sm w-full bg-[#68d391] rounded text-white cursor-pointer" on:click={addCounter}>new counter</button>
  <p>title list: {counters.map(counter => counter.title).join(', ')}</p>
  <p>sum of count: {counters.reduce((sum, { count }) => sum + count, 0)}</p>
</div>
