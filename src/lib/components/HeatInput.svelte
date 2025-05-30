<script lang="ts">
  let { name, value = $bindable(), onInputChange } = $props();

  function handleInput() {
    if (onInputChange) {
      onInputChange(name.toLowerCase());
    }
  }
</script>

<div class="flex max-w-84 w-screen h-14  justify-between items-center">
  <p class="text-lg font-semibold">{name}</p>  <input
    type="number"
    bind:value
    oninput={handleInput}
    placeholder={`Enter ${name}`}
    class="border border-gray-300 rounded"
  />
</div>