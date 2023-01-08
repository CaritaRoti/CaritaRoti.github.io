<template>
    <h2>status: {{ roverStatus }}</h2>
    <h2>Latest photos taken on: {{ photoDate }}</h2>
    <div v-for="camera in cameras">
        <h2>{{ camera.full_name }}</h2>
    </div>
    <div v-for="imageURL in imageURLs" class="cameraImg">
        <img :src=imageURL>
    </div>
</template>

<script>
import { onMounted } from 'vue';

export default {
    name: 'CuriosityCamera',
    data() {
        return {
            roverStatus: '',
            photoDate: '',
            imageURLs: [],
            apiAddress: 'https://mars-photos.herokuapp.com/api/v1/rovers/curiosity/latest_photos'
        }
    },
    mounted() {
        fetch(this.apiAddress)
            .then(res => res.json())
            .then(data => this.getData(data))
            .catch(err => console.log(err.message))
    },
    methods: {
        /**
         * Updates variables according to the given data
         * @param {*} data
         */
        getData(data) {
            this.roverStatus = data.latest_photos[0].rover.status
            this.photoDate = data.latest_photos[0].earth_date
            for (let i = 0; i < data.latest_photos.length; ++i) {
                this.imageURLs.push(data.latest_photos[i].img_src)
            }
            console.log(this.imageURLs)
            return
        }
    }
    
}

</script>