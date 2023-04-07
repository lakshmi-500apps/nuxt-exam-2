<template>
  <CollectionList
    :getQuestionsList="QuestionsList"
    @openAddQuestionForm="openAddQuestion"
    @questionBankData="getQuestionBankData"
    @openViewForm="openViewSidebar"
  />
  <div v-if="openAddForm">
    <CollectionAdd
      v-if="openAddForm"
      :openAddQuestionForm="openAddForm"
      @formData="saveQuestionFormData"
      @cancel="cancel"
    />
  </div>

  <div v-if="openViewForm">
    <CollectionEdit
      v-if="openViewForm"
      :openViewSidebar="openViewForm"
      :questionBankData="questionBankData"
      @cancel="cancel"
    />
  </div>
</template>
<script setup lan="ts">
import { ref } from "vue";

const QuestionsList = ref([]);
const openAddForm = ref(false);
const openViewForm = ref(false);
let questionBankData = ref({});

const openAddQuestion = (data) => {
  openAddForm.value = data;
};

// Get Questions Data
const { data: items } = await useAuthLazyFetch(
  "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc"
);

QuestionsList.value = items.value;

// Post Call Executed when 'Save' button is clicked in Add Question Sidebar
const saveQuestionFormData = async (data) => {
  const postoptions = {
    body: [data],
  };
  await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/bulk",
    postoptions
  );
  openAddForm.value = false;
  // Update QuestionsList Data after inserting a new value
  const { data: response } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  QuestionsList.value = response.value;
};

// Close AddSidebar when Cancel  button clicked
const cancel = () => {
  openAddForm.value = false;
  openViewForm.value = false;
};

// Open View Question Sidebar
const openViewSidebar = (data) => {
  openViewForm.value = data;
};

// To show Data on row click of Question
const getQuestionBankData = (data) => {
  questionBankData.value = data;
};
</script>
