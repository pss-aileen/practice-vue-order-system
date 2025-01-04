<script setup lang="ts">
import { ref, type Ref } from 'vue'

type productType = {
  name: string
  category: string
  description: string
  price: number
  stock: number
  imageUrl: string
}

const products: Ref<productType[]> = ref([])
const productName = ref('test name')
const productCategory = ref('food')
const productDescription = ref('test desc')
const productPrice = ref(100)
const productStock = ref(10)
const productImage = ref('https://placehold.jp/150x150.png')

function addProduct(e: Event) {
  e.preventDefault()

  const product: productType = {
    name: productName.value,
    category: productCategory.value,
    description: productDescription.value,
    price: productPrice.value,
    stock: productStock.value,
    imageUrl: productImage.value,
  }
  console.table(product)
  products.value.push(product)
}
</script>

<template>
  <section class="flex gap-0 text-zinc-800">
    <header class="bg-indigo-800 p-8 text-white">
      <h1 class="font-bold">
        <div class="text-lg">Product Add System</div>
        <div class="text-sm">Demo</div>
      </h1>
    </header>

    <main class="flex-1 min-h-svh p-8">
      <section class="">
        <h2 class="text-xl font-bold">ADD PRODUCT</h2>

        <form @submit="addProduct" class="mt-4 flex gap-6">
          <!-- left -->
          <div class="flex-1">
            <section class="p-4 border rounded">
              <h3 class="font-bold">General Information</h3>
              <div class="mt-2">
                <label class="text-xs text-zinc-600">Product Id</label>
                <div class="mt-1">
                  <input
                    type="text"
                    value="PDC-A-00001"
                    disabled
                    class="bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                  />
                </div>
              </div>
              <div class="mt-2">
                <label class="text-xs text-zinc-600">Name</label>
                <div class="">
                  <input
                    type="text"
                    v-model.trim="productName"
                    class="bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                  />
                </div>
              </div>
              <div class="mt-2">
                <label class="text-xs text-zinc-600">Description</label>
                <div>
                  <textarea
                    name=""
                    id=""
                    v-model="productDescription"
                    class="bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                    rows="4"
                  ></textarea>
                </div>
              </div>
            </section>
            <section class="p-4 border rounded mt-6">
              <h3 class="font-bold">Pricing</h3>
            </section>
            <section class="p-4 border rounded mt-6">
              <h3 class="font-bold">Invently</h3>
            </section>
            <section class="p-4 border rounded mt-6">
              <h3 class="font-bold">Category</h3>
            </section>
            <div>
              <label class="text-xs text-zinc-600">category</label>
              <div>
                <select name="" id="" v-model="productCategory">
                  <option value="food">food</option>
                  <option value="beverage">beverage</option>
                </select>
                <!-- カテゴリー追加画面も作る -->
              </div>
            </div>

            <div>
              <label class="text-xs text-zinc-600">price</label>
              <div>
                <input type="number" v-model="productPrice" />
                円
              </div>
            </div>
            <div>
              <label class="text-xs text-zinc-600">stock</label>
              <div><input type="number" v-model="productStock" /></div>
            </div>
            <section class="buttons">
              <button type="submit">追加</button>
              <button>リセット</button>
            </section>
          </div>
          <!-- right -->
          <div class="flex-1">
            <div>
              <label class="text-xs text-zinc-600">image</label>
              <div>
                <!-- https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/file -->
                <!-- input fileだとローカルストレージに画像保存大変なので、一旦URL保存して呼び出すタイプにする -->
                <input type="text" v-model="productImage" />
                <img :src="productImage" alt="" width="100" height="100" />
              </div>
            </div>
          </div>
        </form>
      </section>
      <section class="product-list-control">
        <h2>Filter & Sort</h2>
      </section>
      <section class="product-list">
        <h2>PRODUCT LIST</h2>

        <table>
          <thead>
            <tr>
              <th>img</th>
              <th>name</th>
              <th>description</th>
              <th>price</th>
              <th>stock</th>
              <th>category</th>
              <th>edit</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="product in products" :key="product.name">
              <td class="image">
                <img :src="product.imageUrl" alt="" width="48" height="48" />
              </td>
              <td class="name">
                <div>{{ product.name }}</div>
              </td>
              <td class="description">
                <div>{{ product.description }}</div>
              </td>
              <td class="price">{{ product.price }}</td>
              <td class="stock">{{ product.stock }}</td>
              <td class="category">{{ product.category }}</td>
              <td class="edit"><button>📝</button></td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>
  </section>
  <footer class="bg-zinc-50 text-zinc-500 text-sm p-4 text-center">
    (c) Product Add System Demo
  </footer>
</template>

<style scoped></style>
