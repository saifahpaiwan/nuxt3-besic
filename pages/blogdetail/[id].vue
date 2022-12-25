<script setup lang="ts">
    // อ่าน id ที่ส่งมา //
    const route = useRoute()
    // console.log(route.params.id)
    const { data: products, pending } = await useFetch(`https://www.itgenius.co.th/sandbox_api/mrta_flutter_api/public/api/news/${route.params.id}`)
    // console.log(products)

    useHead({
        title: `${products.value.topic}`,
        meta: [
            { 
            name: 'keywords', 
            content: `${products.value.topic}`
            },
            {
            name: 'Description',
            content: `${products.value.detail}`
            }
        ]
    }) 
</script>
<template>
    <div class="mb-5">
        <div v-if="!pending"> 
            <div class="wrapper">
                <v-row justify="center">
                <v-col cols="12" sm="10" md="9" lg="7">
                    <div class="text-center">
                    <h2 class="ui-title font-weight-bold text-white mb-4 mt-5"> {{ products.topic }} </h2>
                    </div>
                </v-col>
                </v-row>
            </div>

            <client-only> 
            <v-container>
                <img :src="products.imageurl" class="w-100" :alt="products.topic">
                <h3> รายละเอียดข่าว : {{ products.detail }} </h3>
                <p> วันที่ {{ products.created_at }} </p>
                <a :href="products.linkurl"> อ่านเพิ่มเติม </a>
                <!-- <a @click="$router.go(-1)">back</a> -->
            </v-container> 
            </client-only>
        </div>
        <div class="text-center py-10" v-else> loading... </div>
    </div>
</template>
 
<style scoped>
    .ui-title {
        font-size: 32px;
    }

    .font-18{
        font-size: 18px;
    }

    .wrapper {
        background: #2196F3;
        padding: 40px 0 20px;
        min-height: 250px;
        display: flex;
        align-items: center;
        margin-bottom: 20px;
    }

    .blog-card {
        transition: 0.2s ease-in;
    }

    .blog-card:hover {
        transform: translateY(-10px);
    }

    .blog-title {
        color: #263238 !important;
        line-height: 22px;
        font-weight: bold;
    }

    .blog-title:hover {
        color: #607df9 !important;
    }
 
</style>