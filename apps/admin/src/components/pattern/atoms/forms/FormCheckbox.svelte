<script>
  export let id;
  export let checked = false;
</script>

<input
  {id}
  type="checkbox"
  class="w-4 h-4 bg-gray-50 rounded border border-gray-300 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800"
  bind:checked
/>
