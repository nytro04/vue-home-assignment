<template>
  <div class="container py-5">
    <ShortText ref="short-modal" />
    <LongText ref="long-modal" />
    <SingleChoice ref="single-choice" />
    <!-- <modal name="short-modal" /> -->
    <!-- <modal ref="short-modal"></modal> -->
    <div class="dropdown text-right">
      <a class="btn btn-dark dropdown-toggle" href="#" role="button" id="dropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        Add a question
      </a>

      <div class="dropdown-menu" aria-labelledby="dropdownMenuLink">
        <!--
        <router-link class="dropdown-item" :to="{ name: 'ShortText' }"
          >Short Text</router-link> -->
        <button class="dropdown-item" v-b-modal.modal-prevent-closing>
          Short Text
        </button>
        <button class="dropdown-item" v-b-modal.long-survey-text>
          Long Text
        </button>
        <button class="dropdown-item" v-b-modal.single-choice-survey>
          Single Choice
        </button>
      </div>
    </div>

    <div class="py-5">
      <ul>
        <li v-for="(question, index) in questions" :key="index">
          <p class="question__light">{{ index + 1 }} → {{ question.name }}</p>
          <p class="question__normal">{{ question.label }} ?</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import ShortText from "../components/ShortText";
import LongText from "../components/LongText";
import SingleChoice from "../components/SingleChoice";

export default {
  name: "AddSurvey",
  components: {
    ShortText,
    LongText,
    SingleChoice
  },
  data() {
    return {
      questions: JSON.parse(localStorage.getItem("survey"))
    };
  },

  methods: {}
};
</script>

<style lang="scss" scoped>
li {
  list-style: none;
}

.question {
  &__light {
    font-weight: 300;
    font-size: 0.7rem;
    text-transform: uppercase;
    margin-bottom: 0.3rem;
  }

  &__normal {
  }
}
</style>
