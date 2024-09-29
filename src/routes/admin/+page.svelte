<script>
  import { onMount } from "svelte";
  let products = [];
  let newProduct = { name: "", price: 0 };

  onMount(async () => {
    const response = await fetch("http://localhost:3000/products");
    products = await response.json();
  });

  async function addProduct() {
    const response = await fetch("http://localhost:3000/products", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(newProduct),
    });

    if (response.ok) {
      products.push(await response.json());
      newProduct = { name: "", price: 0 }; // Сбросить форму
    }
  }
</script>

<main class="p-4">
  <h1 class="text-3xl font-bold">Админ панель</h1>

  <h2 class="text-2xl mt-4">Добавить продукт</h2>
  <div class="form-control">
    <label class="label">
      <span class="label-text">Название продукта</span>
    </label>
    <input
      type="text"
      bind:value={newProduct.name}
      class="input input-bordered"
    />

    <label class="label">
      <span class="label-text">Цена продукта</span>
    </label>
    <input
      type="number"
      bind:value={newProduct.price}
      class="input input-bordered"
    />

    <button class="btn btn-primary mt-4" on:click={addProduct}
      >Добавить продукт</button
    >
  </div>

  <h2 class="text-2xl mt-4">Список продуктов</h2>
  <div class="mt-4">
    {#each products as product}
      <div class="card w-full bg-base-100 shadow-xl mb-2">
        <div class="card-body">
          <h2 class="card-title">{product.name}</h2>
          <p>Цена: {product.price} руб.</p>
        </div>
      </div>
    {/each}
  </div>
</main>
