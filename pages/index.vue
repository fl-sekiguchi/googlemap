<template>
  <section class="container">
    <div>
      <div class="map" ref="googleMap"></div>
    </div>
  </section>
</template>

<script>
import GoogleMapsApiLoader from 'google-maps-api-loader';

export default {
  data() {
    return {
      propertys: [
        {
          location: {lat: 35.6754288, lng: 139.7085995},
          name: 'ZOOM神宮前',
          image: 'https://www.zoomrent.jp/wp-content/uploads/2020/01/%E5%A4%96%E8%A6%B3_%E7%A5%9E%E5%AE%AE%E5%89%8D.jpg',
          url: 'https://www.zoomrent.jp/rent/zoom%e7%a5%9e%e5%ae%ae%e5%89%8d/'
        },
        {
          location: {lat: 35.6644964, lng: 139.6909383},
          name: 'ZOOM渋谷神山町',
          image: 'https://www.zoomrent.jp/wp-content/uploads/2020/01/%E5%A4%96%E8%A6%B3_%E6%B8%8B%E8%B0%B7%E7%A5%9E%E5%B1%B1%E7%94%BA.jpg',
          url: 'https://www.zoomrent.jp/rent/zoom%e6%b8%8b%e8%b0%b7%e7%a5%9e%e5%b1%b1%e7%94%ba/'
        },
        {
          location: {lat: 35.6786091, lng: 139.6682946},
          name: 'ZOOM渋谷笹塚',
          image: 'https://www.zoomrent.jp/wp-content/uploads/2020/01/%E5%A4%96%E8%A6%B3_%E6%B8%8B%E8%B0%B7%E7%AC%B9%E5%A1%9A.jpg',
          url: 'https://www.zoomrent.jp/rent/zoom%e6%b8%8b%e8%b0%b7%e7%ac%b9%e5%a1%9a/'
        }
      ],
      google: null
    }
  },
  methods: {
    initializeMap() {
      const map = new this.google.maps.Map(this.$refs.googleMap, {
        center: this.propertys[1].location,
        zoom: 17
      });

      this.propertys.reduce((_, value, index) => {
        const marker = new this.google.maps.Marker({
          position: value.location,
          map: map,
          animation: google.maps.Animation.DROP,
          icon: new google.maps.MarkerImage(
            '/pin.png'
          )
        });

        const infowindow = new this.google.maps.InfoWindow();
        this.google.maps.event.addListener(marker, 'click', e => {
            infowindow.setContent(`<div class="infoWindow"><a href="${value.url}" target="_blank"><img src="${value.image}">${value.name}</a></div>`);
            infowindow.open(map, marker);
        });

      }, undefined);
    }
  },
  async mounted() {
    this.google = await GoogleMapsApiLoader({
      apiKey: 'AIzaSyCMkz1weDQddUD1xEO88dlJIvr0zcWSRSc'
    });
    this.initializeMap();
  }
}
</script>

<style>
.map {
  width: 100vw;
  height: 100vh;
}
.infoWindow a {
  display: block;
  text-align: center;
}
.infoWindow img {
  max-width: 100px;
  margin: 0 auto;
  display: block;
}
</style>

