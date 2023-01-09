<template>
    <div id="mission-info">
        <span id="rover-status"><b>Rover status:</b> {{ roverStatus }}</span>
        <span id="photo-date"><b>Latest photos taken on:</b> {{ photoDate }}</span>
    </div>
    
    <div v-for="camera in cameras">
        <h2>{{ camera.full_name }}</h2>
    </div>
    <div v-for="(imageURLs, cameraName) in images">
        <curiosity-accordion class="accordion">
            <template v-slot:title>
                <span class="button-normaltext">Photos from</span>
                <span class="colored-text"> {{ cameraName }} </span>
                <span class="button normaltext"> ({{ imageURLs.length }})</span>
            </template>
            <template v-slot:content>
                <div class="grid-container">
                    <img v-for="imageURL in imageURLs" :src=imageURL class="rover-img">
                </div>
            </template>
        </curiosity-accordion>
    </div>
    
</template>

<script>
import CuriosityAccordion from './CuriosityAccordion.vue';

export default {
    name: 'CuriosityCamera',
    data() {
        return {
            roverStatus: '',
            photoDate: '',
            imageURLs: [],
            images: {},
            showImages: false,
            apiAddress: 'https://mars-photos.herokuapp.com/api/v1/rovers/curiosity/latest_photos'
        }
    },
    mounted() {
        fetch(this.apiAddress)
            .then(res => res.json())
            .then(data => this.getData(data))
            .catch(err => console.log(err.message))
    },
    components: {
        CuriosityAccordion
    },
    methods: {
        /**
         * Updates variables according to the given data
         * @param {*} data
         */
        getData(data) {
            this.roverStatus = data.latest_photos[0].rover.status;
            this.photoDate = data.latest_photos[0].earth_date;

            for (let i = 0; i < data.latest_photos.length; ++i) {
                let cameraName = data.latest_photos[i].camera.full_name;
                let imgUrl = data.latest_photos[i].img_src;

                (this.images[cameraName] || (this.images[cameraName] = []))
                    .push(imgUrl);
                
            }
            console.log(this.images)
            return
        },

        /**
         * Toggles image showing
         */
        toggleShowImages() {
            this.showImages = !this.showImages
        }
    }
    
}
</script>

<style>
    #mission-info {
        display: flex;
        justify-content: center;
    }

    #rover-status {
        margin-inline: 2%;
    }

    #photo-date {
        margin-inline: 2%;
    }

    .accordion {
        margin: 1%;
    }

    button {
        width: 100%;
        height: 50px;
        padding: 1%;
        font-size: medium;
        
        line-height: 150%;
        display: flex;
        align-items: center;
        background-color: #393939;
        border-color: transparent;
    }

    .button-normaltext {
        color: white;
        font-weight: normal;
        margin-right: 4px;
    }

    .colored-text {
        font-weight: 600;
        color: #6fe5b0;
        margin-right: 4px;
    }

    .rover-img {
        width: 200px;
        margin: 5px;
        display: flexbox;
        justify-content: center;
    }
</style>