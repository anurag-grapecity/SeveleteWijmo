<script lang="ts">
  import "@mescius/wijmo.styles/wijmo.css";
  import { FlexGrid } from "@mescius/wijmo.grid";
  import { onMount } from "svelte";
  import "@mescius/wijmo.styles/themes/wijmo.theme.material.css";

  var countries: Array<string> = "US,Germany,UK,Japan,Italy,Greece".split(",");
  var data: Array<{
    id: number;
    country: string;
    sales: number;
    expenses: number;
  }> = [];

  let grid: FlexGrid | undefined;
  let gridContainer: HTMLElement | null = null;

  onMount(() => {
    for (var i = 0; i < countries.length; i++) {
      data.push({
        id: i,
        country: countries[i],
        sales: Math.random() * 10000,
        expenses: Math.random() * 5000,
      });
    }
    if (gridContainer) {
      grid = new FlexGrid(gridContainer, {
        autoGenerateColumns: false,
        columns: [
          { binding: "id", header: "Id", width: 60 },
          { binding: "country", header: "Country", width: 150 },
          { binding: "sales", header: "Sales", width: 120, format: "n2" },
          {
            binding: "expenses",
            header: "Expenses",
            width: 120,
            format: "n2",
          },
        ],
        itemsSource: data,
      });
    }
  });
</script>

<div class="container-fluid">
  <div class="grid-container" bind:this={gridContainer}></div>
</div>

<style>
  .grid-container {
    max-height: 250px;
    width: fit-content;
    margin: 20px;
  }

  .container-fluid {
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>
