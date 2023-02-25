<template>
    <div>
        
        <b-overlay @click="onclickCard" :show="show" rounded="sm" class="text-center justify-content-center">
            <template #overlay>
                <div> 
                </div>
            </template>
            <img class="showcenter " :src="imageCardUrl" alt="">
            <b-container class="bv-example-row">
                <b-row  class="my-2">
                    <b-col v-for="item in items" :key="item.card_images" class="my-2">
                        <img class="myImg" @click="onclickCard(item.card_images)" :src="item.card_images" width="200" />
                    </b-col>
                </b-row>
            </b-container>
        </b-overlay>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: "TableCenter",
    data() {

        return {
            imageCardUrl:"",
            show: false,
            fields: [

                {
                    key: 'card_images',
                    label: 'Name',
                    thClass: 'text-center',
                    tdClass: 'text-center align-middle text-capitalize'
                },
                {
                    key: 'card_images',
                    label: 'Name',
                    thClass: 'text-center',
                    tdClass: 'text-center align-middle text-capitalize'
                },

            ],
            items: [],
        }
    },
    mounted() {

        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=100&offset=0')
            .then((card) => {
                this.items = card.data.data.map((item) => ({
                    card_images: item.card_images[0].image_url,
                   
                }))
                console.log(card.data.data)
            })

    },
    methods: {
        onclickCard(url) {
            this.imageCardUrl = url
            this.show = !this.show
            document.querySelector('body').style.overflow = this.show ? 'hidden' : "scroll";
            
        }
    }
}
</script>

<style>
.myImg:hover {
    opacity: 1;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s;

}

.myImg {
    opacity: 0.8;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s;
}

.b-overlay {
    background-color: rgb(99, 97, 97, 0.100);
    
    
}

.showcenter  {
    z-index: 9999;
    transform: translate(-50%, -50%);
    position: absolute;
}
</style>