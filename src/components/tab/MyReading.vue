<template>
  <Loading v-if="isLoading" />
  <div v-else class="view d-flex flex-1-0 flex-column">
    <div v-if="myReadingList.length === 0" class="d-flex justify-center align-center">
      <p><span>읽은 책을 추가해서</span>나만의 독서 기록을 만들어봐요😉</p>
    </div>
    <v-list v-else class="d-flex flex-wrap pa-0 pt-8 px-sm-8">
      <MyReadingBook />
    </v-list>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useRecordStore } from '@/stores/record';
import Loading from '@/components/loading/Loading.vue';
import MyReadingBook from '@/components/card/MyReadingBook.vue';

const { inquiryMyReading } = useRecordStore();
const isLoading = computed(() => useRecordStore().isLoading);
const myReadingList = computed(() => useRecordStore().myReadingList);
inquiryMyReading();
</script>

<style scoped>
.view {
  overflow: auto;
}
</style>