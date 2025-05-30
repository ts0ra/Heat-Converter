<script lang="ts">
  let { name, value = $bindable() } = $props();
</script>

<div class="flex max-w-84 w-screen h-14  justify-between items-center">
  <p class="text-lg font-semibold">{name}</p>
  <input
    type="number"
    bind:value
    placeholder={`Enter ${name}`}
    class="border border-gray-300 rounded"
  />
</div>