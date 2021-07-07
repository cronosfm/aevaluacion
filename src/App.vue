<template>
  <div class="mainContainer">
    <div>
      <Button
        v-bind:style="{ 'background-color': colores[0].color }"
        @click="activar(0)"
      ></Button>
      <Button
        v-bind:style="{ 'background-color': colores[1].color }"
        @click="activar(1)"
      ></Button>
    </div>
    <div>
      <div></div>
      <Button
        v-bind:style="{ 'background-color': colores[2].color }"
        @click="activar(2)"
      ></Button>
      <div></div>
    </div>
    <div>
      <Button
        v-bind:style="{ 'background-color': colores[3].color }"
        @click="activar(3)"
      ></Button>
      <Button id="button" v-on:Click="crearSecuencia"> Iniciar </Button>
      <Button
        v-bind:style="{ 'background-color': colores[4].color }"
        @click="activar(4)"
      ></Button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      secuencia: [],
      colores: [
        { id: 0, color: "#FFFFFF" },
        { id: 1, color: "#FFFFFF" },
        { id: 2, color: "#FFFFFF" },
        { id: 3, color: "#FFFFFF" },
        { id: 4, color: "#FFFFFF" },
      ],
    };
  },

  methods: {
    async getColor(value) {
      var auxColor;
      switch (value) {
        case 0:
          auxColor = "#00FF00";
          break;
        case 1:
          auxColor = "#FF0000";
          break;
        case 2:
          auxColor = "#0000FF";
          break;
        case 3:
          auxColor = "#F0F000";
          break;
        case 4:
          auxColor = "#00F0F0";
          break;

        default:
          auxColor = "#FFFFFF";
          break;
      }
      return auxColor;
    },
    async activar(value) {
      var auxColor = await this.getColor(value);
      this.colores[value].color = auxColor;
      setInterval(() => {
        this.colores[value].color = "#FFFFFF";
      }, 1000);
    },
    crearSecuencia() {
      this.secuencia = [];
      for (let index = 0; index < 5; index++) {
        var rnd = Math.floor(Math.random() * (4 - 0)) + 0;
        this.secuencia.push(rnd);
      }
      this.comenzarRonda();
    },
    comenzarRonda() {
      console.log(this.secuencia);
      for (let index = 0; index < this.secuencia.length; index++) {
        const element = this.secuencia[index];
        this.getColor(element).then((colornew) => {
          setInterval(() => {
            this.colores[element].color = colornew;
            setInterval(() => {
              
              this.colores[element].color = "#FFFFFF";
            }, 1000);
          }, 1000);
        });
      }
    },
  },
};
</script>

<style>
.mainContainer {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 98vh;
  overflow: auto;
  background-color: lightblue;
}
.mainContainer div {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
#button {
  background-color: darkorange;
  width: 10%;
  height: 20%;
}
.mainContainer div button {
  background-color: white;
  height: 30vh;
  width: 33%;
}
</style>
