<template>
    <div>
        <b-overlay @click="onclickCard" :show="show" rounded="sm" class="text-center py-3">
            <template #overlay>
                <div>
                </div>
            </template>
            <div class="mt-3 text-center">
                <h6>Page Card</h6>
                <div>
                    <b-pagination @page-click="onChangPage" v-model="currentPage" pills :total-rows="rows"
                        align="center"></b-pagination>
                </div>
            </div>

            <img class="showcenter" :src="imageCardUrl" alt="">
            <b-container class="bv-example-row">
                <b-row>

                    <b-button v-if="loaded" variant="primary" disabled>
                        <b-spinner small type="grow"></b-spinner>
                        Loading...
                    </b-button>

                    <b-col v-for="item in items" :key="item.card_images" v-else class="my-2" md="3" cols="6" >
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
            loaded: false,
            offset: 0,
            rows: 1000,
            currentPage: 1,
            imageCardUrl: "",
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

        this.getData()

    },
    methods: {
        onclickCard(url) {
            this.imageCardUrl = url
            this.show = !this.show
            document.querySelector('body').style.overflow = this.show ? 'hidden' : "scroll";

        },
        onChangPage(event, page) {
            this.offset = (page * 20) - 20

            this.getData()
        },
        getData() {
            this.loaded = true
            axios.get(`https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=${this.offset}`)
                .then((card) => {
                    this.items = card.data.data.map((item) => ({
                        card_images: item.card_images[0].image_url,
                    }))
                    this.loaded = false
                    console.log(card.data.data)
                })
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

.showcenter {
    z-index: 9999;
    transform: translate(-50%, 0%);
    position: fixed;
}
</style>