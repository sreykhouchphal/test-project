<template>
  <div>
    <h2>Products:</h2>
    <div>
      <label for="searchId">Search by ID:</label>
      <input type="number" id="searchId" v-model="searchId" />
      <button @click="searchById">Search</button>
    </div>
    <div>
      <label for="searchCategory">Search by Category:</label>
      <select id="searchCategory" v-model="searchCategory">
        <option value="">All</option>
        <option
          v-for="category in categories"
          :value="category.id"
          :key="category.id"
        >
          {{ category.name }}
        </option>
      </select>
      <button @click="searchByCategory">Search</button>
    </div>
    <ul>
      <li v-for="product in filteredProducts" :key="product.id">
        {{ product.name }} (Category:
        {{ getCategoryName(product.category_id) }})
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: "Dell", category_id: 101 },
        { id: 2, name: "Power Supply", category_id: 102 },
        { id: 3, name: "Macbook", category_id: 101 },
        { id: 4, name: "Monitor", category_id: 103 },
        { id: 5, name: "Keyboard", category_id: 104 },
        { id: 6, name: "Mouse", category_id: 104 },
        { id: 7, name: "Headphones", category_id: 105 },
      ],
      categories: [
        { id: 101, name: "Computers" },
        { id: 102, name: "Power Supplies" },
        { id: 103, name: "Monitors" },
        { id: 104, name: "Mice and Keyboards" },
      ],
      filteredProducts: [],
      searchId: null,
      searchCategory: null,
    };
  },
  computed: {
    getCategoryName() {
      return function (categoryId) {
        const category = this.categories.find(
          (category) => category.id === categoryId
        );
        return category ? category.name : "";
      };
    },
  },
  // methods: {
  //   searchById() {
  //     this.filteredProducts = this.products.filter((product) => product.id === this.searchId);
  //   },
  //   searchByCategory() {
  //     if (this.searchCategory) {
  //       this.filteredProducts = this.products.filter((product) => product.category_id === this.searchCategory);
  //     } else {
  //       this.filteredProducts = this.products;
  //     }
  //   },
  // },
  methods: {
    searchById() {
      this.filteredProducts = [];
      for (let i = 0; i < this.products.length; i++) {
        const product = this.products[i];
        if (product.id === this.searchId) {
          this.filteredProducts.push(product);
        }
      }
    },
    searchByCategory() {
      this.filteredProducts = [];
      if (this.searchCategory) {
        for (let i = 0; i < this.products.length; i++) {
          const product = this.products[i];
          if (product.category_id === this.searchCategory) {
            this.filteredProducts.push(product);
          }
        }
      } else {
        this.filteredProducts = this.products;
      }
    },
  },
};
</script>
