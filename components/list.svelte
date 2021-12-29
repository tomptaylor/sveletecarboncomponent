<script>
  import { DataTable } from "carbon-components-svelte";
  import { DataTableSkeleton } from "carbon-components-svelte";

  async function fetchData() {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();

    if (res.ok) return data;
    else throw new Error(data);
  }
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://unpkg.com/carbon-components@10.21.0/css/carbon-components.min.css" />
</svelte:head>

{#await fetchData()}
  <DataTableSkeleton showHeader={false} showToolbar={false} />
  <!-- <DataTableSkeleton headers={['userId', 'id', 'title', 'cccc']} rows={10} /> -->
{:then rows}
	<DataTable
	size="short"
	headers={[{ key: 'userId', value: 'userId' },{ key: 'id', value: 'Id' }, { key: 'title', value: 'Title' }, { key: 'completed', value: "Completed"}]}
	{rows}
	/>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}



  
  