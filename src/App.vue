<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h1>대충 제목 들어갈곳</h1>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main
      id="content"
      class="d-flex flex-column align-center mt-8"
    >
      <v-spacer>

      </v-spacer>

      <h1
        v-if="!showResult"
        class="mt-4 mb-2"
      >
        {{ address }}
      </h1>

      <v-card
        id="map"
        class="mt-4"
        elevation="1"
      >
        <KakaoMap v-model="geolocation"/>
      </v-card>
      <v-btn
        v-if="!showResult"
        width="100%"
        class="mt-8 mb-10"
        @click="search"
      >
        주소 변경
      </v-btn>
      <div
        v-if="!showResult"
        class="d-flex flex-column align-center"
      >
        <p>{{ building }}</p>
        <v-container fluid>
          <v-row
            class="d-flex justify-space-around"
          >
            <v-checkbox
              v-model="building"
              label="버거"
              value="burger"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
          </v-row>
        </v-container>
        <v-container fluid>
          <v-row
            class="d-flex justify-space-around"
          >
            <v-checkbox
              v-model="building"
              label="버거"
              value="burger"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
          </v-row>
        </v-container>
        <v-container fluid>
          <v-row
            class="d-flex justify-space-around"
          >
            <v-checkbox
              v-model="building"
              label="버거"
              value="burger"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
            <v-checkbox
              v-model="building"
              label="편의점"
              value="cvs"
            ></v-checkbox>
          </v-row>
        </v-container>
        <v-btn
          width="100%"
          color="mt-8 mb-10 primary"
          @click="search"
        >
          몇 세권인지 확인해보기
        </v-btn>
      </div>

      <h1
        v-if="showResult"
        class="mt-4 mb-2"
      >
        {{ address }}은/는 {{ searchResult.length }}세권 입니다.
      </h1>
      <div
        v-if="showResult"
        class="d-flex flex-column align-center"
      >
        <v-card
          class="mt-2 mb-10"
          width="100%"
          outlined
        >
          <v-list-item
            two-line
            v-for="(item, index) in searchResult"
            :key="index"
          >
            <v-list-item-content>
              <v-list-item-title
                class="text-h4 font-weight-bold"
              >
                {{ item.title }}
              </v-list-item-title>
              <v-list-item-subtitle
                class="text-h6 font-weight-bold"
              >
                {{ item.buildingName }}
              </v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </div>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import { Getter } from 'vuex-class';
import KakaoMap from './components/KakaoMap.vue';

@Component({
  components: {
    KakaoMap,
  },
})
export default class App extends Vue {
  @Getter('isLogined')
  private isLogined!: boolean;

  private building: string[] = [];

  private address = '대충 주소';

  private showResult = false;

  private searchResult: Record<string, string>[] = [
    {
      title: '편세권',
      buildingName: '세븐일레븐 무슨무슨점',
    },
    {
      title: '편세권',
      buildingName: '세븐일레븐 무슨무슨점',
    },
    {
      title: '편세권',
      buildingName: '세븐일레븐 무슨무슨점',
    },
    {
      title: '편세권',
      buildingName: '세븐일레븐 무슨무슨점',
    },
  ];

  private geolocation = {
    latitude: 37,
    longitude: 126,
  };

  search() {
    this.showResult = true;
  }
}
</script>

<style scoped>
  #map {
    width: 70vw;
    height: 50vh;
  }
</style>
