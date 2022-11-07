<template>
    <section class="store-products">
        <ul v-for="(product, index) in products" :key="index">
            <ul v-for="(category, index) in product.categories" :key="index">
                <li>{{category.name.uk}}</li>
            </ul>
            <li class="store-products__item">{{product.sku}}</li>
            <li class="store-products__item">{{product.name.uk}}</li>
        </ul>
    </section>
</template>

<script>

    export default {
        name: 'store-products',
        components: {},
        props: {
            products: {
                type: Array,
                default() {
                    return []
                }
            }
        },
    }
</script>

<style scoped>
    .store-products__item {
        padding: 10px 0px 0px 70px;
    }
</style>