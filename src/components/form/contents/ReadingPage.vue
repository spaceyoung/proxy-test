<template>
  <div>
    <span class="d-flex align-center mb-3">
      <v-icon icon="mdi-book-edit-outline" class="mr-2" />독서량
    </span>
    <div class="d-flex">
      <v-text-field v-model.number="book.readingPage" :rules="numberRule" class="flex-0-0 mr-5"
        oninput="this.value = this.value.replace(/[^0-9]/g, '')" placeholder="읽은 페이지 수" hint="숫자만 입력 가능해요."
        variant="solo" flat persistent-hint @blur="autoReadingDone" />
      <span class="flex-1-0 align-self-center"> / {{ book.page }}쪽</span>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  book: { type: Object, required: true },
});

const numberRule = [
  value => !!value || '읽은 페이지수를 입력해주세요.',
  value => value <= props.book.page || `${props.book.page} 이하의 숫자만 입력 가능해요.`
];
const autoReadingDone = () => {
  if (props.book.readingPage === props.book.page) props.book.readingState = '독서 완료';
};
</script>

<style scoped>
.v-text-field {
  width: 210px;
}
.v-text-field + span {
  color: #555;
}
</style>