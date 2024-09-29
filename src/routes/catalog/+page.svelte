<script>
  import { onMount } from "svelte";
  let products = [];

  onMount(async () => {
    const response = await fetch("http://localhost:3000/products");
    products = await response.json();
  });
</script>

<main class="p-4">
  <h1 class="text-3xl font-bold">Каталог продуктов</h1>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
    {#each products as product}
      <div class="card w-full bg-base-100 shadow-xl">
        <div class="card-body">
          <h2 class="card-title">{product.Name}</h2>
          <p>Цена: {product.Price} руб.</p>
        </div>
      </div>
    {/each}
  </div>
</main>
