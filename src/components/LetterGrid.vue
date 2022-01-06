<template>
  <div class="table-container">
    <table>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('00') ? 'green' : 'gray',
              rightLetter.includes('00') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[0][0] ? letterArray[0][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('01') ? 'green' : 'gray',
              rightLetter.includes('01') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[0][1] ? letterArray[0][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('02') ? 'green' : 'gray',
              rightLetter.includes('02') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[0][2] ? letterArray[0][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('03') ? 'green' : 'gray',
              rightLetter.includes('03') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[0][3] ? letterArray[0][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('04') ? 'green' : 'gray',
              rightLetter.includes('04') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[0][4] ? letterArray[0][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('10') ? 'green' : 'gray',
              rightLetter.includes('10') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[1][0] ? letterArray[1][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('11') ? 'green' : 'gray',
              rightLetter.includes('11') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[1][1] ? letterArray[1][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('12') ? 'green' : 'gray',
              rightLetter.includes('12') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[1][2] ? letterArray[1][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('13') ? 'green' : 'gray',
              rightLetter.includes('13') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[1][3] ? letterArray[1][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('14') ? 'green' : 'gray',
              rightLetter.includes('14') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[1][4] ? letterArray[1][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('20') ? 'green' : 'gray',
              rightLetter.includes('20') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[2][0] ? letterArray[2][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('21') ? 'green' : 'gray',
              rightLetter.includes('21') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[2][1] ? letterArray[2][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('22') ? 'green' : 'gray',
              rightLetter.includes('22') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[2][2] ? letterArray[2][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('23') ? 'green' : 'gray',
              rightLetter.includes('23') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[2][3] ? letterArray[2][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('24') ? 'green' : 'gray',
              rightLetter.includes('24') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[2][4] ? letterArray[2][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('30') ? 'green' : 'gray',
              rightLetter.includes('30') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[3][0] ? letterArray[3][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('31') ? 'green' : 'gray',
              rightLetter.includes('31') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[3][1] ? letterArray[3][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('32') ? 'green' : 'gray',
              rightLetter.includes('32') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[3][2] ? letterArray[3][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('33') ? 'green' : 'gray',
              rightLetter.includes('33') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[3][3] ? letterArray[3][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('34') ? 'green' : 'gray',
              rightLetter.includes('34') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[3][4] ? letterArray[3][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('40') ? 'green' : 'gray',
              rightLetter.includes('40') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[4][0] ? letterArray[4][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('41') ? 'green' : 'gray',
              rightLetter.includes('41') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[4][1] ? letterArray[4][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('42') ? 'green' : 'gray',
              rightLetter.includes('42') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[4][2] ? letterArray[4][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('43') ? 'green' : 'gray',
              rightLetter.includes('43') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[4][3] ? letterArray[4][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('44') ? 'green' : 'gray',
              rightLetter.includes('44') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[4][4] ? letterArray[4][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('50') ? 'green' : 'gray',
              rightLetter.includes('50') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[5][0] ? letterArray[5][0].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('51') ? 'green' : 'gray',
              rightLetter.includes('51') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[5][1] ? letterArray[5][1].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('52') ? 'green' : 'gray',
              rightLetter.includes('52') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[5][2] ? letterArray[5][2].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('53') ? 'green' : 'gray',
              rightLetter.includes('53') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[5][3] ? letterArray[5][3].toUpperCase() : "" }}
          </div>
        </td>
        <td>
          <div
            v-bind:class="[
              rightSpot.includes('54') ? 'green' : 'gray',
              rightLetter.includes('54') ? 'yellow' : 'gray',
            ]"
            class="tile"
          >
            {{ letterArray[5][4] ? letterArray[5][4].toUpperCase() : "" }}
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "LetterGrid",
  props: ["letterArray", "rightSpot", "rightLetter"],
};
</script>

<style scoped>
.table-container {
  margin: 0;
  padding: 15px;
}
table {
  margin: 0 auto;
}
.tile {
  width: 50px;
  height: 50px;
  border: 2px solid black;
  color: white;
  font-size: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
}
.gray {
  background-color: #3a3a3c;
}
.green {
  background-color: green;
}
.yellow {
  background-color: #B59F3A;
}
</style>
