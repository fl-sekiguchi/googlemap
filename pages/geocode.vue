<template>
  <section class="container">
    <div>
      <h1>住所から緯度経度を算出して表示（ZOOM神宮前、ZOOM渋谷神山町、ZOOM渋谷笹塚）</h1>
      <p>住所から緯度経度を算出するためにAPIを物件の数分リクエストしなければいけない</p>
      <table>
        <thead>
          <tr>
            <th>用途</th>
            <th>API利用数</th>
            <th>API利用量/月</th>
            <th>API利用単価</th>
            <th>利用金額/月</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>地図の表示</td>
            <td>1</td>
            <td>1,000</td>
            <td>$7/1000回</td>
            <td>$7</td>
          </tr>
          <tr>
            <td>住所から緯度経度算出</td>
            <td>3（物件数）</td>
            <td>1,000</td>
            <td>$5/1000回</td>
            <td>$15</td>
          </tr>
          <tr class="sum">
            <td></td>
            <td></td>
            <td></td>
            <td>合計金額</td>
            <td>$22</td>
          </tr>
          <tr class="sum">
            <td></td>
            <td></td>
            <td></td>
            <td>無償分</td>
            <td>-$200</td>
          </tr>
          <tr class="sum">
            <td></td>
            <td></td>
            <td></td>
            <td>請求金額</td>
            <td>-$178</td>
          </tr>
        </tbody>
      </table>
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
          current: false,
          address: '東京都渋谷区千駄ヶ谷２丁目28-3',
          name: 'ZOOM神宮前',
          image: 'https://www.zoomrent.jp/wp-content/uploads/2020/01/%E5%A4%96%E8%A6%B3_%E7%A5%9E%E5%AE%AE%E5%89%8D.jpg',
          url: 'https://www.zoomrent.jp/rent/zoom%e7%a5%9e%e5%ae%ae%e5%89%8d/'
        },
        {
          current: true,
          address: '東京都渋谷区神山町17-1',
          name: 'ZOOM渋谷神山町',
          image: 'https://www.zoomrent.jp/wp-content/uploads/2020/01/%E5%A4%96%E8%A6%B3_%E6%B8%8B%E8%B0%B7%E7%A5%9E%E5%B1%B1%E7%94%BA.jpg',
          url: 'https://www.zoomrent.jp/rent/zoom%e6%b8%8b%e8%b0%b7%e7%a5%9e%e5%b1%b1%e7%94%ba/'
        },
        {
          current: false,
          address: '東京都渋谷区幡ヶ谷３丁目37-16',
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
        zoom: 17
      });

      this.propertys.reduce((_, value, index) => {
        const geocoder = new google.maps.Geocoder();
        geocoder.geocode({"address" : value.address}, function(results, status) {
          if (status == google.maps.GeocoderStatus.OK) {
            const lat = results[0].geometry.location.lat();
            const lng = results[0].geometry.location.lng();
            const mark = {
              lat: lat,
              lng: lng
            }

            const marker = new this.google.maps.Marker({
              position: mark,
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

            if (value.current) {
              map.setCenter(mark);
            }
          }
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
  width: 600px;
  height: 450px;
}
table {
  border-collapse: collapse;
}
th, td {
  border: 1px solid #000;
  padding: 5px;
}
table tr.sum td {
  border: none;
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

