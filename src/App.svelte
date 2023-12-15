<script>
  import { onMount } from "svelte";
  import tabs from "./data.json";

  let tabOptions = tabs.tabOptions;
  let activeTab = "Home";

  // Maintain separate states for toggle switches
  let toggleSwitchStates = {};
  let showCheckmark = false;

  function openPage(pageName) {
    activeTab = pageName;
    console.log(pageName);
  }

  function toggleSwitchChanged(tabType, event) {
    toggleSwitchStates[tabType] = event.target.checked;

    // Set showCheckmark to true if the current tab's toggle switch is checked
    showCheckmark = toggleSwitchStates[activeTab];

    // Reset the checkmark after 2 seconds
    setTimeout(() => {
      showCheckmark = false;
    }, 2000);
  }

  onMount(() => {
    openPage(activeTab);
  });
</script>

<main>
  <div class="container flex items-center justify-center">
    {#each tabOptions as tabOption}
      <button
        class="tablink bg-[#a0bfd4] font-semibold text-white float-left cursor-pointer p-3 text-lg w-full"
        on:click={() => openPage(tabOption.type)}>{tabOption.type}</button
      >
    {/each}
  </div>

  {#each tabOptions as tabOption}
    {#if activeTab === tabOption.type}
      <div class="tab-container flex flex-col p-8 m-3">
        <div class="tabcontent text-black block flex items-center mb-2 h-full">
          <h3 class="px-2">{tabOption.type}</h3>

          <!-- Toggle Switch -->
          <label class="toggle-switch">
            <input
              type="checkbox"
              bind:checked={toggleSwitchStates[tabOption.type]}
              on:change={(event) => toggleSwitchChanged(tabOption.type, event)}
            />
            <span class="toggle-switch-slider"></span>
          </label>

          <!-- Checkmark -->
          {#if showCheckmark}
            <span class="checkmark px-2 text-base"
              ><img
                class="checkmark-img w-4 h-4"
                src="src/assets/accept.png"
                alt=""
              /></span
            >{/if}
        </div>

        <div class="tab-select flex flex-row block w-60 py-4">
          <label for="pet-select" class="mr-4">Your Options</label>

          <select
            name="pets"
            id="pet-select"
            class="select-options border border-solid border-[#1e3d52] bg-[#a0bfd46a] text-[#1e3d52]"
          >
            <option value="">--Please choose an option--</option>

            {#each tabOption.options as selectOption}
              <option value="">{selectOption}</option>
            {/each}
          </select>
        </div>

        <div class="tab-input flex flex-row block w-50">
          <label for="pet-select" class="pr-4">Write something:</label>
          <input
            type="text"
            class="select-input"
            placeholder="Write something"
          />
        </div>
      </div>
    {/if}
  {/each}
</main>
