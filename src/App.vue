<template>
  <div class="wrapper">
    <select v-model="selectedCategory">
      <option value="">All Categories</option>
      <option v-for="category in uniqueCategories" :key="category" :value="category">{{ category }}</option>
    </select>
    <input v-model="searchInput" @input="searchProducts" placeholder="Search by product name">
    <div class="products-container" v-if="filteredProducts.length">
      <div class="productCard" v-for="product in filteredProducts" :key="product.id" @mouseenter="onMouseEnter(product)">
        <img :src="product.image" :alt="product.prodName">
        <h3>{{ product.prodName }}</h3>
        <p>Category: {{ product.category }}</p>
        <p>Amount: {{ product.amount }}</p>
      </div>
    </div>
    <div v-else>
      <h2>Sorry, no products found</h2>
    </div>v
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      products: [
        {
          id: 1,
          prodName: 'HP Mono LaserJet MFP 137fnw Printer',
          category: 'Gadget',
          amount: 5309.00,
          image: 'https://tech.co.za/wp-content/uploads/2022/02/4ZB84Aa-768x576.jpg'
        },
        {
          id: 2,
          prodName: 'Corsair TC200 Gaming Chair – Soft Fabric – ',
          category: 'Gadget',
          amount: 7759.00,
          image: 'https://tech.co.za/wp-content/uploads/2023/02/CF-9010049-WWa-768x576.png'
        },
        {
          id: 3,
          prodName: 'Dell P2418HT Touch Monitor – 23.8',
          category: 'Gadget',
          amount: 5819.00,
          image: 'https://tech.co.za/wp-content/uploads/2019/06/DELL-P2418HT-510x383.jpg'
        },
        {
          id: 4,
          prodName: 'Asus Vivobook Pro 15 K6502ZC 15.6″ Laptop',
          category: 'Gadget',
          amount: 24159.00,
          image: 'https://tech.co.za/wp-content/uploads/2023/07/Vivobook-Pro-15-K6502ZCa-768x576.png'
        },
        {
          id: 5, 
          prodName: 'Logitech MK330 Wireless Keyboard and Mouse',
          category: 'Gadget',
          amount: 699.00,
          image: 'https://www.firstshop.co.za/cdn/shop/products/920-003989-keyboards-35708394340516_700x.jpg?v=1673263740'
        },
      ],
      selectedCategory: '',
      searchInput: ''
    }
  },
  computed: {
    uniqueCategories() {
      return [...new Set(this.products.map(product => product.category))];
    },
    filteredProducts() {
      let filtered = this.products;

      if (this.selectedCategory) {
        filtered = filtered.filter(product => product.category === this.selectedCategory);
      }
      if (this.searchInput) {
        const searchQuery = this.searchInput.toLowerCase();
        filtered = filtered.filter(product => product.prodName.toLowerCase().includes(searchQuery));
      }
      return filtered;
    }
  },
  methods: {
    onMouseEnter(product) {
      alert(`Hello there! You hovered over ${product.prodName}`);
    },
    searchProducts() {
    }
  }
}
</script>

<style scoped>

img {
  width: 17rem;
}

.products-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.productCard {
  flex: 0 0 calc(33.33% - 20px);
  margin-bottom: 20px;
}
</style>


