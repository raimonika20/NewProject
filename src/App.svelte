<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import options from "./data.json";

  let tabOptions = options.tabOptions;

  let activeTab = "Home";
  let toggleStates = {};

  tabOptions.forEach((tabOption) => {
    toggleStates[tabOption.id] = writable(false);
    toggleStates[`show${tabOption.type}Tick`] = writable(false);
  });

  function openPage(pageName) {
    activeTab = pageName;
    console.log(pageName);
  }

  // Automatically click the default tab on component mount
  onMount(() => {
    document.getElementById("defaultOpen").click();
  });

  // Subscribe to the toggle change and show tick when it's ON
  $: if (toggleStates[`${activeTab.toLowerCase()}Toggle`]) {
    toggleStates[`show${activeTab}Tick`].set(true);

    // Clear the existing timeout to avoid multiple setTimeouts
    setTimeout(() => toggleStates[`show${activeTab}Tick`].set(false), 2000);
  }
</script>

<main>
  {#each tabOptions as tabOption}
    <button
      class="tablink bg-[#395f79] font-semibold text-white float-left cursor-pointer p-3 text-lg w-1/3"
      on:click={() => openPage(tabOption.type)}>{tabOption.type}</button
    >
  {/each}

  {#each tabOptions as tabOption}
    {#if activeTab === tabOption.type}
      <div id={tabOption.type} class="tabcontent text-black block p-20 h-full">
        <h3>{tabOption.type}</h3>
        <label class="switch">
          <input
            type="checkbox"
            bind:checked={toggleStates[`${tabOption.id}Toggle`]}
          />
          <span class="slider round"></span>
        </label>
        {#if toggleStates[`show${tabOption.type}Tick`] && toggleStates[`${tabOption.id}Toggle`]}
          <span class="tick font-bold text-green-600 mx-2.5">✓</span>
        {/if}
      </div>
    {/if}
  {/each}
</main>
