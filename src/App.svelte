<script>
  import { onMount } from "svelte";
  import options from "./data.json";

  let tabOptions = options.tabOptions;
  let activeTab = "Home";
  let selectedOption = null;

  function openPage(pageName) {
    activeTab = pageName;
    console.log(pageName);
  }

  function handleRadioChange(event) {
    selectedOption = event.target.value;

    // Set the checkmark to appear
    setTimeout(() => {
      selectedOption = null; // Reset the selectedOption after 2 seconds
    }, 2000);
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
      <div id={tabOption.type} class="tabcontent text-black block p-10 h-full">
        <h3>{tabOption.type}</h3>

        <!-- Add radio buttons here -->
        <div class="radio-container flex flex-col my-3">
          <label class="radio-option flex items-center mb-2">
            <input
              type="radio"
              name="option"
              value="Option 1"
              on:change={handleRadioChange}
              checked={selectedOption === "Option 1"}
            />Option 1
            {#if selectedOption === "Option 1"}<span
                class="checkmark mr-2 text-[#008000] text-base font-extrabold"
                >&#10003;</span
              >{/if}
          </label>
          <label class="radio-option">
            <input
              type="radio"
              name="option"
              value="Option 2"
              on:change={handleRadioChange}
              checked={selectedOption === "Option 2"}
            />Option 2
            {#if selectedOption === "Option 2"}<span
                class="checkmark mr-2 text-[#008000] text-base font-extrabold"
                >&#10003;</span
              >{/if}
          </label>
        </div>
      </div>
    {/if}
  {/each}
</main>
