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
  <section class="wrapper">
    <header>
      <h1>Product Add System Demo</h1>
    </header>

    <main>
      <section class="add-product">
        <h2>ADD PRODUCT</h2>

        <form @submit="addProduct">
          <table>
            <tbody>
              <tr>
                <th>product id</th>
                <td><input type="text" value="PDC-A-00001" disabled /></td>
              </tr>
              <tr>
                <th>name</th>
                <td>
                  <input type="text" v-model.trim="productName" />
                </td>
              </tr>
              <tr>
                <th>category</th>
                <td>
                  <select name="" id="" v-model="productCategory">
                    <option value="food">food</option>
                    <option value="beverage">beverage</option>
                  </select>
                  <!-- カテゴリー追加画面も作る -->
                </td>
              </tr>
              <tr>
                <th>description</th>
                <td>
                  <textarea name="" id="" v-model="productDescription"></textarea>
                  <p>1000文字以内</p>
                </td>
              </tr>
              <tr>
                <th>price</th>
                <td>
                  <input type="number" v-model="productPrice" />
                  円
                </td>
              </tr>
              <tr>
                <th>stock</th>
                <td><input type="number" v-model="productStock" /></td>
              </tr>
              <tr>
                <th>image</th>
                <td>
                  <!-- https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/file -->
                  <!-- input fileだとローカルストレージに画像保存大変なので、一旦URL保存して呼び出すタイプにする -->
                  <input type="text" v-model="productImage" />
                  <img :src="productImage" alt="" width="100" height="100" />
                </td>
              </tr>
            </tbody>
          </table>

          <section class="buttons">
            <button type="submit">追加</button>
            <button>リセット</button>
          </section>
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
</template>

<style scoped>
.wrapper {
  max-width: 960px;
  margin: 0 auto 80px;

  header {
    padding: 16px 0;
    background: #eee;
    h1 {
      font-size: 32px;
    }
  }

  .add-product {
    margin-top: 48px;
    form {
      margin-top: 16px;
      table {
        width: 100%;
        border-collapse: collapse;
        tbody {
          tr {
            th,
            td {
              padding: 8px;
              border: 1px solid #ccc;
            }
            th {
            }
            td {
              input {
                width: 100%;
              }
              textarea {
                width: 100%;
              }
            }
          }
        }
      }

      .buttons {
        margin-top: 16px;
        text-align: center;

        button {
          display: inline-block;
          width: 100%;
          max-width: 160px;
          padding: 8px 16px;
          background: #eee;
        }

        button + button {
          margin-left: 16px;
        }
      }
    }
  }

  .product-list-control {
    margin-top: 48px;
  }

  .product-list {
    margin-top: 48px;
    table {
      margin-top: 16px;
      width: 100%;
      border-collapse: collapse;
      tr {
        th {
          background: #eee;
        }
        th,
        td {
          padding: 8px;
          border: 1px solid #ccc;
        }
      }
      tbody {
        .image {
          width: calc(48px + 16px);
          text-align: center;

          img {
            object-fit: cover;
          }
        }

        .name {
        }
        .description {
        }
        .price {
          width: 80px;
          text-align: center;
        }
        .stock {
          width: 80px;
          text-align: center;
        }
        .category {
          width: 80px;
          text-align: center;
        }
        .edit {
          width: 48px;
          text-align: center;
        }
      }
    }
  }
}
</style>
