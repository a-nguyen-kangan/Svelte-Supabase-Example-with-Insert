<script>

import { createClient } from '@supabase/supabase-js'

// Create a single supabase client for interacting with your database
const supabase = createClient('https://tmxakqebnogzcnttsohm.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InRteGFrcWVibm9nemNudHRzb2htIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTE5Nzk3NTksImV4cCI6MjAwNzU1NTc1OX0.MJjJZJUNWp7nIwyEAxRkyZuMdtzyaMYPQKDkgdl-BhM');

let newTitle;

async function getTodos() {
  const { data, error } = await supabase
    .from('TodoItems')
    .select()

  console.log(data)

  if(error) {
    console.log(error);
    throw error;
  }

  return data;
}

async function handleSubmit(event) {
  console.log(newTitle);

  const { error } = await supabase
  .from('TodoItems')
  .insert({ title: newTitle });

  promise = getTodos();
}

let promise = getTodos();

</script>

<main>
<input type="text" id="inp-title" bind:value={newTitle} /><br />
<button on:click={handleSubmit}>submit</button>


<ul>
  {#await promise}
    <p>waiting for data...</p>
  {:then todos}
    {#each todos as todoItem}
      <li>{todoItem.id} {todoItem.title} {todoItem.done}</li>
    {/each}

  {:catch error}
    <p>something went wrong...</p>
  {/await}
</ul>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
