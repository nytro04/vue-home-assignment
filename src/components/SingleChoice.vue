<template>
  <div>
    <b-modal id="single-choice-survey" ref="single-choice" title="Single Choice" @show="resetModal" @hidden="resetModal" @ok="handleOk">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group :state="singleState" label="Please enter your single choice survey question" label-for="single-choice" invalid-feedback="input is required">
          <b-form-input id="single-choice" v-model="single" :state="singleState" required></b-form-input>

        </b-form-group>
      </form>
      <template v-slot:modal-footer="{ ok, cancel }">
        <b-button size="sm" variant="success" @click="ok()">
          Submit
        </b-button>
        <b-button size="sm" variant="danger" @click="cancel()">
          Cancel
        </b-button>
      </template>
    </b-modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      single: "",
      singleState: null
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.singleState = valid;
      return valid;
    },
    resetModal() {
      this.single = "";
      this.singleState = null;
    },
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      // Trigger submit handler
      this.handleSubmit();
    },
    handleSubmit() {
      if (!this.checkFormValidity()) {
        return;
      }

      let surveyDB = JSON.parse(localStorage.getItem("survey"));
      surveyDB = surveyDB ? surveyDB : [];

      const singleSurvey = {
        name: "SINGLE CHOICE",
        label: this.single
      };

      localStorage.setItem(
        "survey",
        JSON.stringify([...surveyDB, singleSurvey])
      );

      this.$emit("reload");

      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("single-choice-survey");
      });
    }
  }
};
</script>
