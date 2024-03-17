<template>
  <div class="form">
    <h1>form page</h1>
    <div class="wrapper">
      <table>
        <th colspan="8">嬰兒出生數按性別、生母原屬國籍（地區）、年齡及教育程度分（按登記）</th>
        <tbody>
          <tr>
            <td>統計年</td>
            <td>區域別</td>
            <td>出生者性別</td>
            <td>生母原屬國籍或地區</td>
            <td>生母年齡</td>
            <td>生母教育程度</td>
            <td>嬰兒出生數</td>
          </tr>
          <tr v-for="(item, index) in data" :key="index">
            <td >{{ item.statistic_yyy }}</td>
            <td >{{ item.site_id }}</td>
            <td >{{ item.birth_sex }}</td>
            <td >{{ item.mother_nation }}</td>
            <td >{{ item.mother_age}}</td>
            <td >{{ item.mother_education}}</td>
            <td >{{ item.birth_count}}</td>
          </tr>
        </tbody>
        <tfoot></tfoot>
      </table>
    </div>
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
    .get('https://www.ris.gov.tw/rs-opendata/api/v1/datastore/ODRP028/112', {})
    .then(res => {
      console.log(res.data);
      data.value = res.data.responseData.slice(0,50);
    })
    .catch(error => console.log('錯誤', error));
}
onMounted(() => {
  infoGet();
  });

return {
  data,
  infoGet,
};}}
</script>
