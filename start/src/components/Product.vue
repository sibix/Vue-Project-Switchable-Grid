<template>
  <div class="switchableGrid">
    <div class="container">
      <!-- top bar -->
      <div class="bar">
        <div class="btnHolder">
          <button @click="layout = 'grid'" :class="{barActive: layout === 'grid'}">
            <i class="fas fa-th"></i> Grid
          </button>
          <button @click="layout = 'list'" :class="{barActive: layout === 'list'}">
            <i class="fas fa-list"></i> List
          </button>
        </div>
      </div>
      <!-- content -->
      <div class="content">
        <!-- grid view -->
        <ul v-if="layout === 'grid'" class="grid">
          <li v-for="content in contents" :key="content.id">
            <div class="image">
              <img :src="content.imageSrc" />
            </div>
          </li>
        </ul>
        <!-- list view -->
        <ul v-if="layout ==='list'" class="list">
          <li v-for="content in contents" :key="content.id">
            <img :src="content.fields.MainImage[0].url" />
            <div class="listContent">
              <h2>Rs {{ content.fields.Price }}</h2>
              <h2>{{ content.fields.ProductName }}</h2>
              <p>{{ content.description }}</p>
              <a class="btn" href="#">Read more</a>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  data() {
    return {
      layout: 'list',
      contents: null,
    }
  },
  // mounted() {
  //   fetch('http://localhost:8080/demo/vue/switchable-grid/api/products.json')
  //     .then(response => this.contents = response)
  //     console.log(this.contents)
  // }
  mounted() {
    fetch('https://api.airtable.com/v0/appQ5A4sEU3uZstcI/PRODUCTS?fields=ProductName&fields=Price&fields=MainImage&fields=Image1&fields=Image2&api_key=keyUop6Ql5CLltnDI')
      //fetch('http://localhost:8080/demo/vue/switchable-grid/api/products.json')
      .then(res => res.json())
      .then(data => this.contents = data.records)
      .catch(err => console.log(err.message))
  }
  
};
</script>
