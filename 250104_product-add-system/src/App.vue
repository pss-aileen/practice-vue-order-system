<script setup lang="ts">
import { computed, ref, type Ref } from 'vue'
import AdminSidebar from './components/AdminSidebar.vue'
import AdminFooter from './components/AdminFooter.vue'

type productType = {
  name: string
  category: string
  description: string
  price: number
  stock: number
  imageUrl: string
}

const products: Ref<productType[]> = ref([])
const productName: Ref<string> = ref('')
const productCategory: Ref<string> = ref('food')
const productDescription: Ref<string> = ref('')
const productPrice: Ref<number> = ref(0)
const productStock: Ref<number> = ref(0)
const productImage: Ref<string> = ref('https://placehold.jp/150x150.png')

const localStorageValue = localStorage.getItem('products')
if (localStorageValue) {
  products.value = JSON.parse(localStorageValue)
}

function updateLocalStorage() {
  localStorage.setItem('products', JSON.stringify(products.value))
  const localStorageValue = localStorage.getItem('products')
  if (localStorageValue) {
    console.log(JSON.parse(localStorageValue))
  }
}

const productImageValidation = computed(() => {
  if (!(productImage.value.startsWith('https://') || productImage.value.startsWith('http://'))) {
    return false
  }
  return true
})

const productNameValidation = computed(() => {
  if (productName.value.length <= 2) {
    return false
  }
  return true
})

function addProduct(e: Event) {
  e.preventDefault()

  if (!productImageValidation.value || !productNameValidation.value) {
    alert('必須項目を入力してください。')
    return
  }

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
  updateLocalStorage()

  productName.value = ''
  productDescription.value = ''
  productPrice.value = 0
  productStock.value = 0
  alert('商品を追加しました。')
}
</script>

<template>
  <section class="flex gap-0 text-zinc-800">
    <AdminSidebar />
    <main class="flex-1 min-h-svh p-8">
      <section class="">
        <h2 class="text-xl font-bold">ADD PRODUCT</h2>

        <div class="mt-4 flex gap-6">
          <!-- left -->
          <div class="flex-[2]">
            <section class="p-4 border rounded-lg">
              <h3 class="font-bold">General Information</h3>
              <label class="block mt-2">
                <span class="text-xs text-zinc-600">Product ID</span>
                <input
                  type="text"
                  value="PDC-A-00001"
                  disabled
                  class="mt-1 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                />
              </label>
              <label class="block mt-2">
                <span class="text-xs text-zinc-600">Name</span>
                <input
                  type="text"
                  v-model.trim="productName"
                  class="mt-1 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                />
                <p class="text-xs mt-2 text-red-600" v-show="productName && !productNameValidation">
                  * 2文字以上入力してください。
                </p>
              </label>
              <label class="block mt-2">
                <span class="text-xs text-zinc-600">Description</span>
                <textarea
                  name=""
                  id=""
                  v-model="productDescription"
                  class="mt-1 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                  rows="5"
                ></textarea>
              </label>
            </section>
            <section class="p-4 border rounded-lg mt-6">
              <h3 class="font-bold">Pricing</h3>
              <div class="grid grid-cols-2 gap-4 mt-2">
                <label>
                  <div class="text-xs text-zinc-600">Base Pricing</div>
                  <input
                    type="number"
                    v-model="productPrice"
                    min="0"
                    max="999999"
                    class="mt-1 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                  />
                </label>
                <label>
                  <div class="text-xs text-zinc-600">Stock</div>
                  <input
                    type="number"
                    v-model="productStock"
                    min="0"
                    max="999999"
                    class="mt-1 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                  />
                </label>
              </div>
            </section>
            <section class="mt-6 text-right">
              <button
                class="border border-red-600 text-red-600 py-2 px-3 text-sm rounded font-bold"
              >
                Delete Product
              </button>
              <button
                class="font-bold py-2 px-3 text-sm rounded bg-sky-600 text-white ml-2"
                @click="addProduct"
              >
                Save Product
              </button>
            </section>
          </div>
          <!-- right -->
          <div class="flex-1">
            <section class="p-4 border rounded-lg">
              <h3 class="font-bold">Image</h3>
              <div class="mt-2">
                <img
                  :src="productImage"
                  alt=""
                  width="240"
                  height="240"
                  class="mx-auto rounded-lg aspect-square object-contain bg-zinc-100 p-4"
                />
                <input
                  type="text"
                  v-model="productImage"
                  class="mt-2 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                />
                <p
                  class="text-xs mt-2 text-red-600"
                  v-show="productImage && !productImageValidation"
                >
                  * http://、https:// ではじまるURLを入力してください。
                </p>
              </div>
            </section>
            <section class="p-4 border rounded-lg mt-6">
              <h3 class="font-bold">Category</h3>
              <div>
                <select
                  name=""
                  id=""
                  v-model="productCategory"
                  class="mt-2 bg-zinc-50 py-1 px-2 border rounded text-sm w-full"
                >
                  <option value="food">food</option>
                  <option value="beverage">beverage</option>
                </select>
                <button class="border py-2 px-3 text-sm rounded mt-2">Add Category</button>
              </div>
            </section>
          </div>
        </div>
      </section>

      <!-- PRODUCT LIST -->
      <section class="mt-16">
        <h2 class="text-xl font-bold">PRODUCT LIST</h2>

        <table class="mt-4 w-full text-sm">
          <thead>
            <tr>
              <th class="font-normal bg-zinc-100 p-4">img</th>
              <th class="font-normal bg-zinc-100 p-4">name</th>
              <th class="font-normal bg-zinc-100 p-4">description</th>
              <th class="font-normal bg-zinc-100 p-4">price</th>
              <th class="font-normal bg-zinc-100 p-4">stock</th>
              <th class="font-normal bg-zinc-100 p-4">category</th>
              <th class="font-normal bg-zinc-100 p-4">edit</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="product in products" :key="product.name">
              <td class="p-4 w-[112px]">
                <img
                  :src="product.imageUrl"
                  alt=""
                  width="80"
                  height="80"
                  class="mx-auto rounded"
                />
              </td>
              <td class="p-4 w-40">
                <div>{{ product.name }}</div>
              </td>
              <td class="p-4">
                <div>{{ product.description ? product.description : 'No description' }}</div>
              </td>
              <td class="p-4 text-center">{{ product.price }}</td>
              <td class="p-4 text-center">{{ product.stock }}</td>
              <td class="p-4 text-center">{{ product.category }}</td>
              <td class="p-4 text-center">
                <button class="border py-2 px-3 text-sm rounded mt-2">Edit</button>
              </td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>
  </section>
  <AdminFooter />
</template>

<style scoped></style>
