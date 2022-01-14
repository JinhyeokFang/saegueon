<template>
  <div id="map" ref="mapContainer">

  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class App extends Vue {
  private map: any;

  private value: {
    latitude: number,
    longitude: number,
  } = {
    latitude: 37,
    longitude: 126,
  };

  async mounted() {
    if (!window.kakao) {
      return;
    }

    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition((position) => {
        const options = {
          center: new window.kakao.maps.LatLng(position.coords.latitude, position.coords.longitude),
          level: 3,
        };

        this.map = new window.kakao.maps.Map((this.$el as HTMLElement), options);

        window.kakao.maps.event.addListener(this.map, 'center_changed', this.centerChanged);
      }, (error) => {
        console.error(error);
      }, {
        enableHighAccuracy: true,
        maximumAge: 0,
        timeout: Infinity,
      });
    } else {
      alert('GPS를 지원하지 않습니다');
    }
  }

  centerChanged() {
    const currentGeoLocation = this.map.getCenter();
    this.value.latitude = currentGeoLocation.getLat();
    this.value.longitude = currentGeoLocation.getLng();

    this.$emit('input', {
      latitude: this.value.latitude,
      longitude: this.value.longitude,
    });
  }
}
</script>

<style scoped>
  #id {
    width: 100%;
    height: 100%;
  }
</style>
