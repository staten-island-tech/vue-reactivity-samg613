<template>
  <div id="header" class="header">
    <h1 class="header__title">Welcome to the Widget Shop</h1>
  </div>

  <div id="filters" class="filters">
    <button class="filters__button" @click="filterWidgets('electronics')">Electronics</button>
    <button class="filters__button" @click="filterWidgets('clothing')">Clothing</button>
    <button class="filters__button" @click="filterWidgets('home')">Home</button>
    <button class="filters__button" @click="filterWidgets('all')">All</button>
  </div>

  <div id="card-container" class="card-container">
    <div v-if="filteredWidgets.length === 0">
      <p class="card-container__empty-message">No widgets found for this category.</p>
    </div>
    <div v-for="widget in filteredWidgets" :key="widget.id" class="card card--effect">
      <img :src="widget.image" :alt="widget.name" class="card__image" />
      <h3 class="card__title">{{ widget.name }}</h3>
      <p class="card__description">{{ widget.description }}</p>
      <p class="card__price">Price: ${{ widget.price.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const widgets = ref([
  {
    id: 1,
    name: 'IPhone 12 Pro Max',
    category: 'electronics',
    price: 999,
    description: 'A high-performance smartphone with cutting-edge features for tech enthusiasts.',
    image:
      'https://th.bing.com/th/id/R.10a14e6394eca91f2d7aeb507e2a347c?rik=9KxLYr1NQjVxeg&pid=ImgRaw&r=0',
  },
  {
    id: 2,
    name: 'Stylish Denim Jacket',
    category: 'clothing',
    price: 79.99,
    description: 'A trendy and comfortable denim jacket, perfect for casual outings.',
    image:
      'https://th.bing.com/th/id/R.f595f6a3c7dc93f4c115322e91ac52bc?rik=5EqrHYXAPh%2bI5w&pid=ImgRaw&r=0',
  },
  {
    id: 3,
    name: 'Airpods',
    category: 'electronics',
    price: 129.99,
    description: 'Experience exceptional sound quality with these sleek and wireless earbuds.',
    image:
      'https://th.bing.com/th/id/R.bb134912948dad2a199eaeaf7e398137?rik=aE6IAsqpJJFpog&riu=http%3a%2f%2fs3.amazonaws.com%2fdigitaltrends-uploads-prod%2f2016%2f12%2fApple-AirPods-kit1.jpg&ehk=b7Upud25GtqHWwuNV%2faUjRVLKC%2fHL%2fGlBh056YVeBqk%3d&risl=&pid=ImgRaw&r=0',
  },
  {
    id: 4,
    name: 'Modern Table Lamp',
    category: 'home',
    price: 49.99,
    description: 'A stylish table lamp that adds a contemporary touch to any room.',
    image:
      'https://th.bing.com/th/id/OIP.4fdl-Q1WGE5YK8d30TnmuAHaHa?w=203&h=203&c=7&r=0&o=5&pid=1.7',
  },
  {
    id: 5,
    name: 'Breathable T-Shirt',
    category: 'clothing',
    price: 19.99,
    description: 'A comfortable and breathable T-shirt made from high-quality cotton.',
    image:
      'https://th.bing.com/th/id/OIP.Y8nGX-1Pb74qFPwBMIFlYgHaLW?w=133&h=205&c=7&r=0&o=5&pid=1.7',
  },
  {
    id: 6,
    name: 'Smartwatch Ultra',
    category: 'electronics',
    price: 249.99,
    description: 'A premium smartwatch with fitness tracking, notifications, and more.',
    image:
      'https://th.bing.com/th/id/OIP.1wvfFeDiDaU-lfB_e9Rq_wHaFj?w=242&h=181&c=7&r=0&o=5&pid=1.7',
  },
  {
    id: 7,
    name: 'Robotic Vacuum Cleaner',
    category: 'home',
    price: 199.99,
    description: 'A powerful robotic vacuum that cleans your home with ease and efficiency.',
    image:
      'https://th.bing.com/th/id/R.b5528ab134607f8d01fb49c2acfde6ed?rik=GLAkwXBmXBmwMg&riu=http%3a%2f%2fwww.christianhomebusinessconnection.com%2fwp-content%2fuploads%2f2016%2f06%2fChoose-Modern-Vacuum-Cleaners.jpg&ehk=7200x5pT6f4BkfnPRbwxcaymCiQFWtmwJjKZg32gy%2bs%3d&risl=&pid=ImgRaw&r=0',
  },
  {
    id: 8,
    name: 'Hoodie',
    category: 'clothing',
    price: 39.99,
    description: 'A soft and cozy hoodie, perfect for lounging or casual wear.',
    image:
      'https://th.bing.com/th/id/R.f2d3746c1f45760eb475c8fd2a2a43d8?rik=cjuDGi8sCaEruQ&pid=ImgRaw&r=0',
  },
  {
    id: 9,
    name: 'Smart Home Hub',
    category: 'home',
    price: 149.99,
    description:
      'The ultimate smart home device that connects and controls all your smart gadgets.',
    image:
      'https://th.bing.com/th/id/OIP.JhrJpAuCXlNueRcS43kC4AHaHk?w=165&h=180&c=7&r=0&o=5&pid=1.7',
  },
])

const selectedCategory = ref('all')

const filteredWidgets = computed(() => {
  if (selectedCategory.value === 'all') {
    return widgets.value
  }
  return widgets.value.filter((widget) => widget.category === selectedCategory.value)
})

function filterWidgets(category) {
  selectedCategory.value = category
}
</script>

<style>
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  --primary-background: #ffffff;
  --primary-text: #213547;
  --button-background: #f9f9f9;
  --button-hover: #747bff;
  --button-text: #213547;
  --link-color: #646cff;
  --link-hover: #747bff;
  --card-text: #213547;
  --card-width: 400px;
  --card-height: 400px;
}

[data-theme='dark'] {
  --primary-background: #2c3e50;
  --primary-text: #ecf0f1;
  --button-background: #1a1a1a;
  --button-hover: #646cff;
  --button-text: #ecf0f1;
  --link-color: #646cff;
  --link-hover: #535bf2;
  --card-text: #ecf0f1;
}

body {
  margin: 0;
  background-color: var(--primary-background);
  color: var(--primary-text);
  font-family: inherit;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: var(--primary-background);
  width: 100%;
}

.header__title {
  font-size: 2em;
  margin: 0;
}

.filters {
  margin: 20px 0;
  text-align: center;
}

.filters__button {
  padding: 0.6em 1.2em;
  margin: 0.5rem;
  background-color: var(--button-background);
  color: var(--button-text);
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.25s;
}

.filters__button:hover {
  background-color: var(--button-hover);
}

.card-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  padding: 2rem;
  margin-top: 20px;
}

.card {
  background-color: var(--primary-background);
  color: var(--card-text);
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: var(--card-width);
  height: var(--card-height);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card__image {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 1rem;
  max-height: 150px;
  object-fit: contain;
}

.card__title {
  font-size: 1.2em;
  margin-bottom: 0.5rem;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.card__description {
  font-size: 0.9em;
  color: #555;
  flex-grow: 1;
}

.card__price {
  font-size: 1em;
  color: #333;
}

.card--effect:hover {
  transform: scale(1.05) translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
}

.card-container__empty-message {
  font-size: 1.2em;
  color: #888;
  text-align: center;
}

@media (max-width: 768px) {
  .card-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .card-container {
    grid-template-columns: 1fr;
  }
}
</style>
