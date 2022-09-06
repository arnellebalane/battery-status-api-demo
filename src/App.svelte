<script>
  import { onMount } from 'svelte';
  import Header from './Header.svelte';
  import Battery from './Battery.svelte';
  import StatusTable from './StatusTable.svelte';

  let isSupported = null;
  let battery = null;
  const events = ['chargingchange', 'chargingtimechange', 'dischargingtimechange', 'levelchange'];

  onMount(async () => {
    isSupported = 'BatteryManager' in window && typeof navigator.getBattery === 'function';

    if (isSupported) {
      battery = await navigator.getBattery();
      events.forEach((event) => {
        battery.addEventListener(event, () => (battery = battery));
      });
    }
  });
</script>

<main class="max-w-xl mx-auto p-6 text-slate-900">
  <Header />
  <Battery bind:battery />
  <StatusTable bind:battery />
</main>
