<script lang="ts">
  import HeatInput from "../lib/components/HeatInput.svelte";
  import Title from "../lib/components/Title.svelte";

  let celcius: number = $state(0);
  let fahrenheit: number = $state(0);
  let kelvin: number = $state(0);
  let lastChanged: string = $state('celsius');

  function handleInputChange(unit: string) {
    lastChanged = unit;
  }

  function updateFromCelsius(value: number) {
    if (value === null || value === undefined || isNaN(value)) {
      fahrenheit = 0;
      kelvin = 0;
      return;
    }
    fahrenheit = parseFloat((((value * 9) / 5) + 32).toFixed(2));
    kelvin = parseFloat((value + 273.15).toFixed(2));
  }

  function updateFromFahrenheit(value: number) {
    if (value === null || value === undefined || isNaN(value)) {
      celcius = 0;
      kelvin = 0;
      return;
    }
    celcius = parseFloat((((value - 32) * 5) / 9).toFixed(2));
    kelvin = parseFloat((celcius + 273.15).toFixed(2));
  }

  function updateFromKelvin(value: number) {
    if (value === null || value === undefined || isNaN(value)) {
      celcius = 0;
      fahrenheit = 0;
      return;
    }
    celcius = parseFloat((value - 273.15).toFixed(2));
    fahrenheit = parseFloat((((celcius * 9) / 5) + 32).toFixed(2));
  }

  $effect(() => {
    if (lastChanged === 'celsius') {
      updateFromCelsius(celcius);
    }
  });

  $effect(() => {
    if (lastChanged === 'fahrenheit') {
      updateFromFahrenheit(fahrenheit);
    }
  });

  $effect(() => {
    if (lastChanged === 'kelvin') {
      updateFromKelvin(kelvin);
    }
  });

</script>

<div class="w-screen h-screen bg-amber-200 flex flex-col items-center justify-center">
  <Title />
  <HeatInput name="Celsius" bind:value={celcius} onInputChange={handleInputChange} />
  <HeatInput name="Fahrenheit" bind:value={fahrenheit} onInputChange={handleInputChange} />
  <HeatInput name="Kelvin" bind:value={kelvin} onInputChange={handleInputChange} />
</div>
