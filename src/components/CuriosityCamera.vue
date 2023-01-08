<template>
    <h2>{{ roverStatus }}</h2>
</template>

<script>
import { onMounted } from 'vue';

export default {
    name: 'CuriosityCamera',
    data() {
        return {
            roverStatus: []
        }
    },
    mounted() {
        fetch('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity?api_key=kssS7ws0hOckIYyOU1hfhv0s3yjGCOam1LypP6r3')
            .then(res => res.json())
            .then(data => this.roverStatus = data.rover.status)
            .catch(err => console.log(err.message))
    }
}

</script>