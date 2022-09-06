<script>
  export let battery;

  $: level = (battery?.level ?? 0) * 100;
</script>

<div class="flex items-center mt-6 mb-16 md:px-12">
  <div class="flex-grow grid h-36 border-8 border-gray-300 rounded-3xl">
    <div
      class="col-span-full row-span-full h-full rounded-2xl "
      class:bg-green-700={battery?.charging}
      class:bg-red-700={!battery?.charging}
      style:width={`${level}%`}
    />
    <h2 class="col-span-full row-span-full place-self-center text-6xl font-bold">{level}%</h2>
  </div>
  <div class="w-8 h-16 rounded-r-lg bg-gray-300" />
</div>
