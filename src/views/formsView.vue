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
    <div class="pageBtnList" v-if="!nodata">
      <button
        class="pageBtn pageBtncursor"
        @click="nextPrevPage('prev')"
        v-if="currentPage != 1"
      >
        ＜
      </button>
      <button
        class="pageBtn"
        v-for="page in totalPages"
        :key="page"
        @click="currentPage !== page ? changePage(item) : null"
        :class="{
          pageBtncursor: currentPage != page,
          currPageBtn: currentPage == page,
        }"
      >
        {{ page }}
      </button>
      <button
        class="pageBtn pageBtncursor"
        @click="nextPrevPage('next')"
        v-if="currentPage != totalPages"
      >
        ＞
      </button>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';

export default {
  setup() {
const data = ref("");
const displayData = ref([]);
const currentPage = ref(1);
const itemsPerPage = ref(50);
const nodata = computed(() => {
  return displayData.value.length == 0;
});

const currentData = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  const end = start + itemsPerPage.value;
  return displayData.value.slice(start, end);
});

const totalPages = computed(() => {
  return Math.ceil( displayData.value.length / this.itemsPerPage);
});

function changePage (item) {
  currentPage.value = item;

};

// 獲取api
function infoGet() {
  axios
    .get('https://www.ris.gov.tw/rs-opendata/api/v1/datastore/ODRP028/112', {})
    .then(res => {
      console.log(res.data);
      data.value = res.data.responseData.slice(0,150);
    })
    .catch(error => console.log('錯誤', error));
}
onMounted(() => {
  infoGet();
  });

return {
  data,
  displayData,
  currentPage,
  itemsPerPage,
  nodata,
  currentData,
  totalPages,
  infoGet,
  changePage,
};}}
</script>
