<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";

  let activeTab = "Home";
  let homeToggle = writable(false);
  let aboutToggle = writable(false);
  let contactToggle = writable(false);
  let showHomeTick = writable(false);
  let showAboutTick = writable(false);
  let showContactTick = writable(false);

  function openPage(pageName) {
    activeTab = pageName;
  }

  // Automatically click the default tab on component mount
  onMount(() => {
    document.getElementById("defaultOpen").click();
  });

  // Subscribe to the toggle change and show tick when it's ON
  $: if ($homeToggle) {
    showHomeTick.set(true);
    setTimeout(() => showHomeTick.set(false), 2000);
  }
  $: if ($aboutToggle) {
    showAboutTick.set(true);
    setTimeout(() => showAboutTick.set(false), 2000);
  }
  $: if ($contactToggle) {
    showContactTick.set(true);
    setTimeout(() => showContactTick.set(false), 2000);
  }
</script>

<main>
  <button
    class="tablink bg-[#395f79] hover:bg--[#1e3d52] font-semibold text-white float-left cursor-pointer p-3 text-lg w-1/3"
    id="defaultOpen"
    on:click={() => openPage("Home")}>Home</button
  >
  <button
    class="tablink bg-[#395f79] hover:bg--[#1e3d52] font-semibold text-white float-left cursor-pointer p-3 text-lg w-1/3"
    on:click={() => openPage("About")}>About</button
  >
  <button
    class="tablink bg-[#395f79] hover:bg--[#1e3d52] font-semibold text-white float-left cursor-pointer p-3 text-lg w-1/3"
    on:click={() => openPage("Contact")}>Contact</button
  >

  {#if activeTab === "Home"}
    <div id="Home" class="tabcontent text-black block p-20 h-full">
      <h3>Home</h3>
      <label class="switch">
        <input type="checkbox" bind:checked={$homeToggle} />
        <span class="slider round"></span>
      </label>
      {#if $showHomeTick}
        <span class="tick font-bold text-green-600 mx-2.5">✓</span>
      {/if}
    </div>
  {/if}

  {#if activeTab === "Contact"}
    <div id="Contact" class="tabcontent text-black block p-20 h-full">
      <h3>Contact</h3>
      <label class="switch">
        <input type="checkbox" bind:checked={$contactToggle} />
        <span class="slider round"></span>
      </label>
      {#if $showContactTick}
        <span class="tick font-bold text-green-600 mx-2.5">✓</span>
      {/if}
    </div>
  {/if}

  {#if activeTab === "About"}
    <div id="About" class="tabcontent text-black block p-20 h-full">
      <h3>About</h3>
      <label class="switch">
        <input type="checkbox" bind:checked={$aboutToggle} />
        <span class="slider round"></span>
      </label>
      {#if $showAboutTick}
        <span class="tick font-bold text-green-600 mx-2.5">✓</span>
      {/if}
    </div>
  {/if}
</main>
