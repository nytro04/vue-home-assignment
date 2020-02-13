<template>
  <div class="container py-5">
    <ShortText ref="short-modal" @reload="reload" />
    <LongText ref="long-modal" @reload="reload" />
    <SingleChoice ref="single-choice" @reload="reload" />
    <div class="dropdown text-right">
      <a class="btn btn-outline-dark dropdown-toggle" href="#" role="button" id="dropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        Add a question
      </a>

      <div class="dropdown-menu" aria-labelledby="dropdownMenuLink">
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
  props: ["questions"],
  name: "AddSurvey",
  components: {
    ShortText,
    LongText,
    SingleChoice
  },
  data() {
    return {};
  },

  methods: {
    reload() {
      this.$emit("updateLS");
    }
  }
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
