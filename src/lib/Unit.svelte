<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let count: number = 0;
  export let title: string = 'new';

  const increment = () => {
    dispatch('increment');
  };

  const decrement = () => {
    dispatch('decrement');
  };

  const reset = () => {
    dispatch('reset');
  };

  const remove = () => {
    dispatch('remove');
  };

  const changeTitle = (event: Event) => {
    const target = event.target as HTMLInputElement; // Type casting
    dispatch('changeTitle', {
      text: target.value,
    });
  };
</script>

<div class="max-w-sm rounded bg-[#f7fafc] shadow-lg m-auto flex relative items-center mb-2">
  <input
    class="text-[#718096] mx-4 px-1 w-32"
    value={title}
    on:input={changeTitle}
  />
  <span class="text-lg font-bold ml-[10px] px-4 text-center">{count}</span>
  <div class="ml-auto flex justify-center items-center my-1">
    <button class="bg-[#F5656C] py-1 px-3 text-[18px] rounded-l text-white" on:click={increment}>+</button>
    <button class="bg-[#4299e1] py-1 px-3 text-[18px] text-white" on:click={decrement}>-</button>
    <button class="bg-[#ecc94b] rounded-r py-1 px-3 text-[18px] text-white" on:click={reset}>0</button>
    <button class="text-[#a0aec0] cursor-pointer px-4" on:click={remove}>x</button>
  </div>
</div>
