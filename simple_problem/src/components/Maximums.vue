<template>
  <div class="main_container">
    <div class="centered_div">
      <p>
        Introduceți un șir de numere cuprinse între 100 și 999 separate prin
        virgulă
      </p>
      <input id="num_input" />
      <button class="calc" @click="findMaximums()">Calculează</button>
      <div class="results">
        Maximele din clase: <b>{{ result.length > 0 ? result : "" }}</b>
        <br />
        Modulo: <b>{{ result.length > 0 ? ciphers : "" }}</b>
        <br />
        <br />
        <ul class="layout">
          <li v-for="elem in elements" :key="elem">
            <div class="matrixCell">
              <div class="cellValue" @click="setValue">?</div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <br />
    <br />
  </div>
</template>

<script>
export default {
  name: "Maximums",
  data() {
    return {
      lista: [
        { class: 100, numbers: [], max: 0 },
        { class: 200, numbers: [], max: 0 },
        { class: 300, numbers: [], max: 0 },
        { class: 400, numbers: [], max: 0 },
        { class: 500, numbers: [], max: 0 },
        { class: 600, numbers: [], max: 0 },
        { class: 700, numbers: [], max: 0 },
        { class: 800, numbers: [], max: 0 },
        { class: 900, numbers: [], max: 0 },
      ],
      elements: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16],
      result: [],
      ciphers: [],
    };
  },
  methods: {
    setValue: function (event) {
      if (event.target.innerText != "?") alert(event.target.innerText);

      let position = Math.floor(Math.random() * this.ciphers.length);
      if (this.ciphers.length > 0) {
        event.target.innerText = this.ciphers[position];
      } else {
        alert("Nu mai există numere în listă");
      }

      this.ciphers.splice(position, 1);
    },
    findMaximums() {
      let arr = [];
      arr = document.getElementById("num_input").value;
      arr = arr.split(" ").join("");
      arr = arr.split(",");

      if (arr.length > 0 && arr[0] !== "") {
        for (let x of arr) {
          for (let i = 0; i < 9; i++) {
            if (x.toString().startsWith((i + 1).toString())) {
              this.lista[i].numbers.push(x);
              this.lista[i].max = Math.max(...this.lista[i].numbers);
            }
          }
        }

        this.result = this.lista
          .filter((e) => e.max != 0)
          .map((elem) => {
            return elem.max;
          });

        this.ciphers = this.result.map((elem) =>
          String.fromCharCode(parseInt(parseInt(elem) % 26) + 65)
        );

        this.lista.map((item) => {
          item.max = 0;
          item.numbers = [];
        });
      } else {
        alert("Introduceți numere în casetă");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.centered_div {
  height: fit-content;
  width: 40vw;
  padding-left: 5px;
  text-align: left;
  display: block !important;
  border: 3px solid #42b983;
  padding-bottom: 1vw;
}

.calc {
  height: 4vh;
  margin-left: 20px;
}

.cellValue {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100% !important;
  width: 100% !important;
  font-size: 3vw;
}

.matrixCell {
  width: 8vw;
  text-align: center;
  margin-bottom: 1vh;
  margin-right: -1.5vh;
  height: 5vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(70, 221, 171, 0.267);
}

.matrixCell:hover {
  background-color: #42b983;
  cursor: pointer;
}

.layout {
  display: flex;
  margin-left: 1vw;
  flex-flow: row wrap;
  flex-direction: row;
}

.results {
  margin-top: 2vh;
  height: fit-content !important;
  width: 95% !important;
  border: 3px groove #8a8888;
  padding: 1vh;
}

#num_input {
  width: 25vw;
  height: 3vh;
  font-size: 15px;
  border: 3px groove #8a8888;
}

.main_container {
  height: 80vh;
  width: 98vw;
  justify-content: center;
  align-items: center;
  display: flex;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
