<template>
  <CollectionList
    :getQuestionsList="QuestionsList"
    @formData="saveQuestionFormData"
  />
 
  <CollectionAdd  />
</template>
<script setup lan="ts">
import { ref } from "vue";

const QuestionsList = ref([]);

let openAddQuestionForm = ref(false);

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

  // Update QuestionsList Data after inserting a new value
  const { data: response } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  QuestionsList.value = response.value;
};
</script>
