<script setup lang="ts"></script>

<template>
  <section class="wrapper">
    <header>
      <h1>Product Add System Demo</h1>
    </header>

    <main>
      <section class="add-product">
        <h2>ADD PRODUCT</h2>

        <form>
          <table>
            <tbody>
              <tr>
                <th>商品名</th>
                <td><input type="text" /></td>
              </tr>
              <tr>
                <th>カテゴリー</th>
                <td>
                  <select name="" id="">
                    <option value="">food</option>
                    <option value="">beverage</option>
                  </select>
                  <!-- カテゴリー追加画面も作る -->
                </td>
              </tr>
              <tr>
                <th>商品説明</th>
                <td>
                  <textarea name="" id=""></textarea>
                  <p>1000文字以内</p>
                </td>
              </tr>
              <tr>
                <th>値段</th>
                <td>
                  <input type="number" />
                  円
                </td>
              </tr>
              <tr>
                <th>1日の在庫数</th>
                <td><input type="number" /></td>
              </tr>
              <tr>
                <th>商品画像</th>
                <td>
                  <input type="file" accept="image/png, image/jpeg" />
                  <!-- https://developer.mozilla.org/ja/docs/Web/HTML/Element/input/file -->
                  とりあえず1枚ということにする
                </td>
              </tr>
            </tbody>
          </table>

          <section class="buttons">
            <button>追加</button>
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
              <th>title & description</th>
              <th>price</th>
              <th>stock</th>
              <th>edit</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <img
                  src="https://images.unsplash.com/photo-1508170754725-6e9a5cfbcabf?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                  alt=""
                  width="80"
                  height="80"
                />
              </td>
              <td>
                <div>お弁当名</div>
                <div>お弁当の詳細</div>
              </td>
              <td>1000</td>
              <td>10/10</td>
              <td><button>編集</button></td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>
  </section>
</template>

<style scoped>
.wrapper {
  max-width: 800px;
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
      tbody {
        tr {
          th,
          td {
            padding: 8px;
            border: 1px solid #ccc;
          }
        }
      }
    }
  }
}
</style>
