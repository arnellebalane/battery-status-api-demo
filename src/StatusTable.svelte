<script>
  export let battery;

  const getReadableTime = (time) => {
    console.log(time);
    if (time === Number.POSITIVE_INFINITY) {
      return 'Unknown';
    }
    const hours = Math.floor(time / 60 / 60);
    const minutes = (time / 60) % 60;
    const seconds = time % 60;
    return [hours ? `${hours}h` : null, `${minutes}m`, `${seconds}s`].filter(Boolean).join(' ');
  };

  $: status = battery
    ? [
        {
          label: 'Is charging?',
          value: battery.charging ? 'Yes' : 'No',
        },
        battery.charging
          ? {
              label: 'Charging time',
              value: getReadableTime(battery.chargingTime),
            }
          : {
              label: 'Discharging time',
              value: getReadableTime(battery.dischargingTime),
            },
      ]
    : [];
</script>

<table class="w-full">
  <tbody>
    {#each status as row}
      <tr>
        <td class="py-2 px-4 border">{row.label}</td>
        <td class="py-2 px-4 border">{row.value}</td>
      </tr>
    {/each}
  </tbody>
</table>
