<template>
  <div class="container mt-5">
    <div class="row">
      <div class="input-group mb-3 text-center justify-content-evenly">
        <div>
          <span class="input-group-text">Escribe el codigo del juego</span>
          <input
            type="text"
            class="form-control text-center"
            placeholder="Ejemplo: 0001"
            v-model="findGameVmodel"
          />
        </div>
        <div class="col-6" v-show="findGameVmodel.length > 3">
          <table class="table" v-for="game in findGameSet" :key="game.codigo">
            <thead>
              <tr>
                <th scope="col" :style="`background-color: ${game.color}`">
                  Codigo
                </th>
                <th scope="col">Nombre</th>
                <th scope="col">Stock</th>
                <th scope="col">Precio</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row">{{ game.codigo }}</th>
                <td>{{ game.nombre }}</td>
                <td>{{ game.stock }}</td>
                <td>${{ game.precio.toLocaleString("DE") }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="row justify-content-center ">
      <div class="col-md-6 d-inline-flex justify-content-evenly">
        <h3><strong>Juegos Registrados: </strong>{{ dataGames.length }}</h3>
        <h3><strong>Stock Total: </strong>{{ stockTotal }}</h3>
      </div>
    </div>
    <div class="row  justify-content-center">
      <div class="col-md-6">
        <GamesList :gameListProps="dataGames" />
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapState } from "vuex";
import GamesList from "@/components/GamesList.vue";
export default {
  name: "BusquedaView",
  data() {
    return {
      findGameVmodel: "",
    };
  },
  computed: {
    ...mapGetters(["stockTotal", "findGame"]),
    ...mapState(["dataGames"]),
    findGameSet() {
      return this.findGame(this.findGameVmodel);
    },
  },
  components: {
    GamesList,
  },
};
</script>

<style></style>
