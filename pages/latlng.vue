<template>
  <section class="container">
    <div>
      <h1>緯度経度を直接指定して表示（ZOOM神宮前、ZOOM渋谷神山町、ZOOM渋谷笹塚）</h1>
      <p>すでに緯度経度がわかっている状態なので、APIで余分なリクエストをしなくてもよい</p>
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
          <tr class="sum">
            <td></td>
            <td></td>
            <td></td>
            <td>合計金額</td>
            <td>$7</td>
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
            <td>-$193</td>
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
        zoom: 17,
        styles: [
  {
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#f5f5f5"
      }
    ]
  },
  {
    "elementType": "labels.icon",
    "stylers": [
      {
        "visibility": "off"
      }
    ]
  },
  {
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#616161"
      }
    ]
  },
  {
    "elementType": "labels.text.stroke",
    "stylers": [
      {
        "color": "#f5f5f5"
      }
    ]
  },
  {
    "featureType": "administrative.land_parcel",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#bdbdbd"
      }
    ]
  },
  {
    "featureType": "poi",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#eeeeee"
      }
    ]
  },
  {
    "featureType": "poi",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#757575"
      }
    ]
  },
  {
    "featureType": "poi.park",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#e5e5e5"
      }
    ]
  },
  {
    "featureType": "poi.park",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#9e9e9e"
      }
    ]
  },
  {
    "featureType": "road",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#ffffff"
      }
    ]
  },
  {
    "featureType": "road.arterial",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#757575"
      }
    ]
  },
  {
    "featureType": "road.highway",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#dadada"
      }
    ]
  },
  {
    "featureType": "road.highway",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#616161"
      }
    ]
  },
  {
    "featureType": "road.local",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#9e9e9e"
      }
    ]
  },
  {
    "featureType": "transit.line",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#e5e5e5"
      }
    ]
  },
  {
    "featureType": "transit.station",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#eeeeee"
      }
    ]
  },
  {
    "featureType": "water",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#c9c9c9"
      }
    ]
  },
  {
    "featureType": "water",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#9e9e9e"
      }
    ]
  }
]
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

        const infowindow = new this.google.maps.InfoWindow({
          disableAutoPan: true
        });
        infowindow.setContent(`<div class="infoWindow"><a href="${value.url}" target="_blank"><img src="${value.image}">${value.name}</a></div>`);
        infowindow.open(map, marker);
      }, undefined);

      map.addListener('dragend', (argument) => {
        // ここで範囲とって再描画
        console.log('dragend')
        const bounds = map.getBounds();
        console.log(bounds.getNorthEast().lat())
        console.log(bounds.getSouthWest().lat())
        console.log(bounds.getNorthEast().lng())
        console.log(bounds.getSouthWest().lng())
      });

      map.addListener('zoom_changed', (argument) => {
        // ここで範囲とって再描画
        console.log('zoom_changed')
        const bounds = map.getBounds();
        console.log(bounds.getNorthEast().lat())
        console.log(bounds.getSouthWest().lat())
        console.log(bounds.getNorthEast().lng())
        console.log(bounds.getSouthWest().lng())
      });
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

