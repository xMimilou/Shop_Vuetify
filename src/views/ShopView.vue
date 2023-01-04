<template>
    <div class="container">
        <!-- for article display v-card-->
        <div v-for="item in items" :key="item.id">
            <v-card
                :loading="loading"
                class="mx-auto my-12"
                max-width="374"
            >
            <template slot="progress">
            <v-progress-linear
                color="deep-purple"
                height="10"
                indeterminate
            ></v-progress-linear>
            </template>

            <v-img fill
            height="250" width="250"
            :src="item.image_path"
            ></v-img>

            <v-card-title>{{ item.article }}</v-card-title>

            <v-card-text>
            <v-row
                align="center"
                class="mx-0"
            >
                <v-rating
                :value="item.rate"
                color="amber"
                dense
                half-increments
                readonly
                size="14"
                ></v-rating>

                <div class="grey--text ms-4">
                {{ item.rate }} ({{ item.nb_rate }})
                </div>
            </v-row>

            <div class="my-4 text-subtitle-1">
                {{ item.price }}$ • {{ item.Company }}
            </div>

            <div>{{ item.Description }}</div>
            </v-card-text>

            <v-divider class="mx-4"></v-divider>

            <v-card-title>Size availability</v-card-title>

            <v-card-text>
            <v-chip-group
                v-model="selection"
                active-class="deep-purple accent-4 white--text"
                column
            >
                <v-chip v-for="size in item.Taille" :id="size">{{ size }}</v-chip>
            </v-chip-group>
            </v-card-text>

            <v-card-actions>
            <v-btn
                color="deep-purple lighten-2"
                text
                @click="AddCart(item.id)"
            >
                Ajouter au panier
            </v-btn>
            </v-card-actions>
            </v-card>
        </div>

    </div>
    
</template>


<script lang="ts">

/* read on display all users present in api localhost:3000/users */
import { defineComponent, ref, onMounted } from 'vue'
import axios from 'axios'
import { Item } from '../@types/item'
export default {
    name: 'UsersView',
    data: () => ({
      loading: false,
      selection: 1,
    }),
    setup() {
        const items = ref([])
        const getUsers = async () => {
        const response = await axios.get('http://localhost:3000/shop')
        items.value = response.data
        console.log(response.data)

        }
        onMounted(getUsers)
        return { items }
    },

    methods: {
      reserve () {
        this.loading = true

        setTimeout(() => (this.loading = false), 2000)
      },
      AddCart(id: number) {
        
      }
    },
  }
</script>



<style scoped>
.container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;

    
}
.container > *{
    margin-top: 5px;
}

.mx-auto {
    margin: 0 auto;
}

.my-12 {
    margin: 3rem 0;
}

.grey--text {
    color: #757575 !important;
}

.ms-4 {
    margin-left: 1.5rem;
}

.deep-purple {
    color: #673ab7 !important;
}
.accent-4 {
    color: #7c4dff !important;
}
.white--text {
    color: #fff !important;
}
.mx-0 {
    margin-left: 0 !important;
    margin-right: 0 !important;
}

.mx-4 {
    margin-left: 1.5rem !important;
    margin-right: 1.5rem !important;
}

.text-subtitle-1 {
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.75;
    letter-spacing: 0.00938em;
}

.lighten-2 {
    color: #9575cd !important;
}
.cover {
    object-fit: fill !important;
}
</style>
