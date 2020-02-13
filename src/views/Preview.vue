<template>
  <div class="container py-5">
    <div class="py-5">
      <ul>
        <li v-for="(question, index) in questions" :key="index">
          <p class="question__normal">
            {{ index + 1 }} → {{ question.label }} ?
          </p>
          <input v-if="question.name === 'SHORT TEXT'" type="text" placeholder="Type your answer here..." />
          <textarea v-if="question.name === 'LONG TEXT'" name="long-text" id="long-text" cols="50" rows="3" placeholder="Type your answer here..."></textarea>
          <template v-if="question.name === 'SINGLE CHOICE'">
            <div class="radiobtn">
              <input type="radio" id="yes" value="Yes" v-model="picked">
              <label for="yes">Yes</label>
            </div>
            <div class="radiobtn">
              <input type="radio" id="no" value="No" v-model="picked">
              <label for="no">No</label>
            </div>
          </template>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["questions"],
  name: "Preview",
  components: {},
  data() {
    return {
      picked: ""
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

input,
input:active,
input:focus,
textarea,
textarea:active,
textarea:focus {
  border-color: #fff;
  outline: none;
}

input[type="text"],
input[type="textarea"],
textarea {
  padding-bottom: 0.5rem;
  border: none;
  border-bottom: 1px solid #e7e7e7;
  width: 70%;
  margin-bottom: 2rem;
}

input[type="radio"] {
  display: none;
}

.radiobtn {
  display: block;

  label {
    border-radius: 5px;
    padding: 0.2rem 3rem;
    border: 1px solid #000;
    text-align: left !important;
    background-color: #eeeeee;
  }
}
</style>
