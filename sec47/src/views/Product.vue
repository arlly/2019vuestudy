<template>
    <div class="product" v-if="item" key="product">
        <h1>商品情報</h1>
        <p>このページはIDが{{ id }}の詳細を表示します。</p>
        <dl class="product-table">
            <dt>商品名</dt>
            <dd>{{ item.name }}</dd>
            <dt>価格</dt>
            <dd>{{ item.price }}</dd>
            <dt>商品説明</dt>
            <dd>{{ item.content }}</dd>
        </dl>
    </div>
    <div v-else key="loading">商品情報を読みこんでいます・・・</div>
</template>

<script>
    import product from '@/api/product.js'

    export default {
        name: "Product",
        props: {
            id: Number
        },
        data() {
            return {
                item: null
            }
        },
        watch: {
            id: {
                handler() {
                    product.asyncFind(this.id, item => {
                        this.item = item
                    })
                }, immediate: true
            }
        }
    }
</script>

<style scoped>

</style>
