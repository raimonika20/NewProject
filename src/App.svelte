<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import options from "./data.json";

  let tabOptions = options.tabOptions;
  let showCheckmark = false;
  let activeTab = "Home";

  function openPage(pageName) {
    activeTab = pageName;

    // Reset the checkmark after 2 seconds
    setTimeout(() => {
      showCheckmark = false;
    }, 2000);

    console.log(pageName);
  }

  // Automatically click the default tab on component mount
  onMount(() => {
    openPage(activeTab);
  });
</script>

<main>
  <div class="container flex items-center justify-center">
    {#each tabOptions as tabOption}
      <button
        class="tablink bg-[#395f79] font-semibold text-white float-left cursor-pointer p-3 text-lg w-full"
        on:click={() => openPage(tabOption.type)}>{tabOption.type}</button
      >
    {/each}
  </div>

  {#each tabOptions as tabOption}
    {#if activeTab === tabOption.type}
      <div class="tabcontent text-black block p-10 h-full">
        <h3>{tabOption.type}</h3>

        <div>
          <label>
            <input type="radio" name="option" value="option1" /> Option 1
          </label><br />
          <label>
            <input type="radio" name="option" value="option2" /> Option 2
          </label>
        </div>
      </div>
    {/if}
  {/each}
</main>
