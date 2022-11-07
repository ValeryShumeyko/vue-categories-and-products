<template>
    <div class="main-wrapper">
        <store-categories
            @sendCategoryId="showId"
        ></store-categories>
        <p v-if="loading">Loading...</p>
        <store-products :products="products"></store-products>
        <p v-if="this.loading===false && this.showCategory && products.length===0">products in this category were not found</p>
    </div>
</template>

<script>
import storeCategories from './store-categories'
import storeProducts from './store-products'
import axios from 'axios'


export default {
    name: 'store-main-wrapper',
    components: {
        storeCategories,
        storeProducts
    },
    props: {},
    data() {
        return {
            categoryId: '',
            products: [],
            loading: false,
            showCategory: false,
            slug: '',
        }
    },
    methods: {
        showId(categoryId, slug) {
            this.products = [];
            this.categoryId = categoryId;
            this.slug = slug;
            this.$router.push(this.slug)
            this.loading=true
                axios
                    .get('https://dev.api.logicpower.ua/user/catalog/product/list/all?pageSize=20&pageNum=1&categoryId=' + `${this.categoryId}`)
                    .then(response => this.products = response.data.data.items)
                    .catch(error => {
                        console.log(error)
                    })
                    .finally(() => (this.loading = false));
            this.showCategory=true;
        },
        watchRouter() {
            this.slug = this.$route.href
        },
    },
    mounted() {
        this.loading=true;
        axios
            .get('https://dev.api.logicpower.ua/user/catalog/product/list/all?pageSize=20&pageNum=1')
            .then(response => this.products = response.data.data.items)
            .catch(error => {
                console.log(error)
            })
            .finally(() => (this.loading = false));
    },
    watch: {
        $route: 'watchRouter'
    },
}
</script>

<style scoped>
.main-wrapper {
    display: flex;
}
</style>