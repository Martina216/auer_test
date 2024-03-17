<template>
  <div class="chart">
    <h1>chart page</h1>
    <!-- <h2>{{data.responseData}}</h2> -->
    <table>
      <caption>嬰兒出生數按性別、生母原屬國籍（地區）、年齡及教育程度分(按登記)</caption>
      <th>hello</th>
      <tbody>
        <tr v-for="(item, index) in data" :key="index">
          <td></td>
        </tr>
      </tbody>
      <tfoot>2</tfoot>
    </table>
  </div>
</template>

<script>
import { ref,onMounted } from 'vue';
import axios from 'axios';


export default {
  setup() {
const data = ref("");

function infoGet() {
  axios
    .get('https://www.ris.gov.tw/rs-opendata/api/v1/datastore/ODRP028/108', {})
    .then(res => {
      console.log(res.data);
      data.value = res.data.responseData.slice(0,10);
    })
    .catch(error => console.log('錯誤', error));
}
onMounted(() => {
  infoGet();
  // console.log(infoGet());
  });

return {
  data,
  infoGet,
};}}


</script>
