<template>
    <section class="store-categories">
        <p v-if="loading">Loading...</p>
        <ul v-for="(category, index) in categories.data" :key="index" class="store-categories__category">
            <li @click="getProductByCategory(category)">{{category.name.uk}}</li>
            <ul v-for="(subcategory, index) in category.children" :key="index" class="store-categories__subcategory">
                <li @click="getProductByCategory(subcategory)">{{subcategory.name.uk}}</li>
                <ul v-for="(subsubcategory, index) in subcategory.children" :key="index" class="store-categories__subsubcategory">
                    <li @click="getProductByCategory(subsubcategory)">{{subsubcategory.name.uk}}</li>
                </ul>
            </ul>
        </ul>
    </section>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'store-categories',
        components: {},
        props: {},
        data() {
            return {
                categories: [],
                loading: true,
                slug: '',
            }
        },
        mounted() {
            axios
                .get('https://dev.api.logicpower.ua/user/catalog/category/list/tree')
                .then(response => this.categories = response.data)
                .catch(error => {
                    console.log(error)
                })
                .finally(() => (this.loading = false));
        },
        methods: {
            getProductByCategory(category) {
                this.$emit('sendCategoryId', category.id, category.slug, category)
            },
            watchRouter() {
                this.slug = this.$route.href;
            },
        },
        watch: {
            $route: [{handler: 'watchRouter'}]
        },
    }
</script>

<style scoped>
.store-categories {
    padding: 0px 230px 0px 0px;
}
.store-categories__category {
    padding: 10px 0px 0px 40px;
}
.store-categories__subcategory {
    padding: 10px 0px 0px 50px;
}
.store-categories__subsubcategory {
    padding: 10px 0px 0px 60px;
}
</style>