<script lang="ts" setup>
  const { data: products, pending } = await useFetch('https://www.itgenius.co.th/sandbox_api/mrta_flutter_api/public/api/news')
  // console.log(products);
    useHead({
        title: 'บล็อก',
        meta: [
            { 
            name: 'keywords', 
            content: 'บล็อก, Nuxt 3, Backend'
            },
            {
            name: 'Description',
            content: 'บล็อก Nuxt 3,  IT Genius Engineering'
            }
        ]
    }) 

    const getDay = (dateText: string) => {
      const date = new Date(dateText)
      return date.getDate()     
    }

    const getMonth = (dateText: string) => {
      const date = new Date(dateText)
      const monthNames = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
      return monthNames[ date.getMonth() ]      
    }
</script>

<template>
    <div class="mb-5">

        <div class="wrapper">
            <v-row justify="center">
            <v-col cols="12" sm="10" md="9" lg="7">
                <div class="text-center">
                <h2 class="ui-title font-weight-bold text-white mb-4">บล็อกล่าสุด</h2>
                <p class="text-white">
                    You can relay on our amazing features list and also our customer services will be great experience for you without doubt and in no-time
                </p>
                </div>
            </v-col>
            </v-row>
        </div>

        <v-container>
          <v-row class="mt-13" justify="center" v-if="!pending">
            
            <v-col cols="12" md="6" lg="4" v-for="(product, index) in products" :key="index">
              <v-card elevation="0" class="blog-card overflow-hidden mb-5" :to="`/blogdetail/${product.id}`">
                <div class="position-relative mb-5">
                  
                    <v-img :src="product.imageurl"
                      alt="blog"
                      class="blog-img"/>
                  
                  <div class="date-badge bg-info-grediant">
                    {{ getMonth(product.created_at) }} <span> {{ getDay(product.created_at) }} </span>
                  </div>
                </div>
                <div class="pa-5">
                  <client-only>
                    <v-card-title class="
                        blog-title
                        text-decoration-none
                        font-weight-medium font-18">
                        {{ product.topic }} 
                    </v-card-title> 
                  </client-only>
                  <client-only>
                    <v-card-subtitle class="mb-10">
                        {{ product.detail }} 
                    </v-card-subtitle>   
                  </client-only>
                </div>
              </v-card>
            </v-col> 

          </v-row>
        <div class="text-center py-10" v-else> loading... </div>
      </v-container>

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
        min-height: 400px;
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