<template>
    <div>
        <Head>
            <Title>
                Nuxt Dojo | {{ product.title }}
                <Meta name="description" :content="product.description"/>
            </Title>
        </Head>
        <ProductDetails :product="product"/>
    </div>
</template>

<script setup>
    const { id } = useRoute().params
    const uri = 'https://fakestoreapi.com/products/' + id

    //fetch product
    const { data: product } = await useFetch(uri, {key: id});
    if (!product.value) {
        throw createError({ statusCode: 404, statusMessage: 'Product not found'})
    }
    definePageMeta ({
        layout: 'products'
    })
</script>

<style scoped>

</style>