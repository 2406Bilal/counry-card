<script lang="ts" setup>
import ProductService from '~~/services/ProductService';

const productService = new ProductService();

useHead({
  title: 'Dashboard'
});

const products = ref([]);
const items = ref([
  { label: 'Add New', icon: 'pi pi-fw pi-plus' },
  { label: 'Remove', icon: 'pi pi-fw pi-minus' }
]);
const lineData = ref({
  labels: ['Russia', 'USA', 'China', 'Canada', 'Japan', 'Korea'],
  datasets: [
    {
      label: 'Revenue',
      data: [65, 59, 80, 81, 56, 55, 40],
      fill: false,
      backgroundColor: '#2f4860',
      borderColor: '#2f4860',
      tension: 0.4
    },
    {
      label: 'Sales',
      data: [28, 48, 40, 19, 86, 27, 90],
      fill: false,
      backgroundColor: '#00bb7e',
      borderColor: '#00bb7e',
      tension: 0.4
    }
  ]
});

function formatCurrency(value) {
  // @ts-ignore
  return value.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
}

onMounted(() => {
  productService.getProductsSmall().then((data) => {
    products.value = data;
  });
});
</script>

<template>
  <div class="grid">
    <div class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">создатель</span>
            <div class="text-900 font-medium text-xl">
              Билол Исмонов
            </div>
          </div>
          <div class="flex align-items-center justify-content-center bg-blue-100 border-round"
            style="width:2.5rem;height:2.5rem">
            <i class="pi pi-shopping-cart text-blue-500 text-xl" />
          </div>
        </div>
        <span class="text-green-500 font-medium">для курсового проекта</span>
        <span class="text-500">программирование на языках высокого уровня</span>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">Получатель</span>
            <div class="text-900 font-medium text-xl">
              Косимов Абдунаби
            </div>
          </div>
          <div class="flex align-items-center justify-content-center bg-orange-100 border-round"
            style="width:2.5rem;height:2.5rem">
            <i class="pi pi-map-marker text-orange-500 text-xl" />
          </div>
        </div>
        <span class="text-green-500 font-medium">Доценть</span>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">Университеть</span>
            <div class="text-900 font-medium text-xl">
              ТТУ
            </div>
          </div>
          <div class="flex align-items-center justify-content-center bg-cyan-100 border-round"
            style="width:2.5rem;height:2.5rem">
            <i class="pi pi-inbox text-cyan-500 text-xl" />
          </div>
        </div>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">Факултуть</span>
            <div class="text-900 font-medium text-xl">
              ИКиТ
            </div>
          </div>
          <div class="flex align-items-center justify-content-center bg-purple-100 border-round"
            style="width:2.5rem;height:2.5rem">
            <i class="pi pi-comment text-purple-500 text-xl" />
          </div>
        </div>
      </div>
    </div>

    <div class="col-12 xl:col-6">
      <div class="card">
        <h5>Recent Sales</h5>
        <DataTable :value="products" :rows="5" :paginator="true" responsive-layout="scroll">
          <Column style="width:15%">
            <template #header>
              Image
            </template>
            <template #body="slotProps">
              <img :src="`/images/product/${slotProps.data.image}`" :alt="slotProps.data.image" width="50"
                class="shadow-2">
            </template>
          </Column>
          <Column field="name" header="Name" :sortable="true" style="width:35%" />
          <Column field="Capital" header="Capital" :sortable="true" style="width:35%">
            <template #body="slotProps">
              {{ formatCurrency(slotProps.data.price) }}
            </template>
          </Column>
          <Column style="width:15%">
            <template #header>
              View
            </template>
            <template #body>
              <Button icon="pi pi-search" type="button" class="p-button-text" />
            </template>
          </Column>
        </DataTable>
      </div>
      <div class="card">
        <div class="flex justify-content-between align-items-center mb-5">
          <h5>странны с болгими тератории </h5>
          <div>
            <Button icon="pi pi-ellipsis-v" class="p-button-text p-button-plain p-button-rounded"
              @click="$refs.menu2.toggle($event)" />
            <ClientOnly>
              <Menu ref="menu2" :popup="true" :model="items" />
            </ClientOnly>
          </div>
        </div>
        <ul class="list-none p-0 m-0">
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Россия</span>
              <div class="mt-1 text-600">
                Москва
              </div>
            </div>
            <div class="mt-2 md:mt-0 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-orange-500 h-full" style="width:50%" />
              </div>
              <span class="text-orange-500 ml-3 font-medium">%50</span>
            </div>
          </li>
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Канада</span>
              <div class="mt-1 text-600">
                Атава
              </div>
            </div>
            <div class="mt-2 md:mt-0 ml-0 md:ml-8 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-cyan-500 h-full" style="width:16%" />
              </div>
              <span class="text-cyan-500 ml-3 font-medium">%16</span>
            </div>
          </li>
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">США</span>
              <div class="mt-1 text-600">
                Вашингтон
              </div>
            </div>
            <div class="mt-2 md:mt-0 ml-0 md:ml-8 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-pink-500 h-full" style="width:67%" />
              </div>
              <span class="text-pink-500 ml-3 font-medium">%67</span>
            </div>
          </li>
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Wonders Notebook</span>
              <div class="mt-1 text-600">
                Office
              </div>
            </div>
            <div class="mt-2 md:mt-0 ml-0 md:ml-8 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-green-500 h-full" style="width:35%" />
              </div>
              <span class="text-green-500 ml-3 font-medium">%35</span>
            </div>
          </li>
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Mat Black Case</span>
              <div class="mt-1 text-600">
                Accessories
              </div>
            </div>
            <div class="mt-2 md:mt-0 ml-0 md:ml-8 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-purple-500 h-full" style="width:75%" />
              </div>
              <span class="text-purple-500 ml-3 font-medium">%75</span>
            </div>
          </li>
          <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
            <div>
              <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Robots T-Shirt</span>
              <div class="mt-1 text-600">
                Clothing
              </div>
            </div>
            <div class="mt-2 md:mt-0 ml-0 md:ml-8 flex align-items-center">
              <div class="surface-300 border-round overflow-hidden w-10rem lg:w-6rem" style="height:8px">
                <div class="bg-teal-500 h-full" style="width:40%" />
              </div>
              <span class="text-teal-500 ml-3 font-medium">%40</span>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div class="col-12 xl:col-6">
      <div class="card">
        <h5>Sales Overview</h5>
        <Chart type="line" :data="lineData" />
      </div>
      <div class="card">
        <div class="flex align-items-center justify-content-between mb-4">
          <h5>Самые богатые странны</h5>
          <div>
            <Button icon="pi pi-ellipsis-v" class="p-button-text p-button-plain p-button-rounded"
              @click="$refs.menu1.toggle($event)" />
            <ClientOnly>
              <Menu ref="menu1" :popup="true" :model="items" />
            </ClientOnly>
          </div>
        </div>

        <span class="block text-600 font-medium mb-3">TODAY</span>
        <ul class="p-0 mx-0 mt-0 mb-4 list-none">
          <li class="flex align-items-center py-2 border-bottom-1 surface-border">
            <div
              class="w-3rem h-3rem flex align-items-center justify-content-center bg-blue-100 border-circle mr-3 flex-shrink-0">
              <i class="pi pi-dollar text-xl text-blue-500" />
            </div>
            <span class="text-900 line-height-3">Катар
              <span class="text-700">has purchased a blue t-shirt for <span class="text-blue-500">79$</span></span>
            </span>
          </li>
          <li class="flex align-items-center py-2">
            <div
              class="w-3rem h-3rem flex align-items-center justify-content-center bg-orange-100 border-circle mr-3 flex-shrink-0">
              <i class="pi pi-download text-xl text-orange-500" />
            </div>
            <span class="text-700 line-height-3">Your request for withdrawal of <span
                class="text-blue-500 font-medium">2500$</span> has been initiated.</span>
          </li>
        </ul>

        <span class="block text-600 font-medium mb-3">YESTERDAY</span>
        <ul class="p-0 m-0 list-none">
          <li class="flex align-items-center py-2 border-bottom-1 surface-border">
            <div
              class="w-3rem h-3rem flex align-items-center justify-content-center bg-blue-100 border-circle mr-3 flex-shrink-0">
              <i class="pi pi-dollar text-xl text-blue-500" />
            </div>
            <span class="text-900 line-height-3">Keyser Wick
              <span class="text-700">has purchased a black jacket for <span class="text-blue-500">59$</span></span>
            </span>
          </li>
          <li class="flex align-items-center py-2 border-bottom-1 surface-border">
            <div
              class="w-3rem h-3rem flex align-items-center justify-content-center bg-pink-100 border-circle mr-3 flex-shrink-0">
              <i class="pi pi-question text-xl text-pink-500" />
            </div>
            <span class="text-900 line-height-3">Jane Davis
              <span class="text-700">has posted a new questions about your product.</span>
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
