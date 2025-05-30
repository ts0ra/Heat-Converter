<script lang="ts">
  import HeatInput from "../lib/components/HeatInput.svelte";
  import Title from "../lib/components/Title.svelte";

  let celcius: number = $state(0);
  let fahrenheit: number = $state(0);
  let kelvin: number = $state(0);

  $effect(() => {
    fahrenheit = parseFloat((((celcius * 9) / 5) + 32).toFixed(2));
    kelvin = parseFloat((celcius + 273.15).toFixed(2));
  });
  $effect(() => {
    celcius = parseFloat((((fahrenheit - 32) * 5) / 9).toFixed(2));
    kelvin = parseFloat((celcius + 273.15).toFixed(2));
  });
  $effect(() => {
    celcius = parseFloat((kelvin - 273.15).toFixed(2));
    fahrenheit = parseFloat((((celcius * 9) / 5) + 32).toFixed(2));
  });

</script>

<div class="container bg-amber-200 flex flex-col items-center justify-center min-h-screen">
  <Title />
  <HeatInput name="Celsius" bind:value={celcius} />
  <HeatInput name="Fahrenheit" bind:value={fahrenheit} />
  <HeatInput name="Kelvin" bind:value={kelvin} />
</div>