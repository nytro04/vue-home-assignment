<template>
  <div>
    <b-modal id="single-choice-survey" ref="single-choice" title="Single Choice" @show="resetModal" @hidden="resetModal" @ok="handleOk">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group :state="singleState" label="Please enter your single choice survey question" invalid-feedback="input is required">
          <b-form-input v-model="single" :state="singleState" required></b-form-input>
        </b-form-group>

        <b-form-group :state="optionsState" label="Please enter your single choice options" invalid-feedback="input is required">
          <b-form-input :key="index" v-model="options" :state="optionsState" required></b-form-input>
          <b-form-text id="password-help-block">
            Your options should be comma seperated. eg. Yes, No, Maybe
          </b-form-text>
        </b-form-group>

        <!-- implementing sleeker add additional input  -->
        <!-- <div v-for="(input, index) in options" :key="index"> -->
        <!-- <b-form-group v-for="(input, index) in options" :key="index" :state="optionsState" label="Please enter your options choice survey question" invalid-feedback="input is required">
          <b-form-input :key="index" v-model="options.name" :state="optionsState" required></b-form-input>
          <span>
            <i class="fas fa-plus" @click="addNewInput(index)" v-show="index == inputs.length-1"></i>
            <i class="fas fa-minus"></i>
          </span>
        </b-form-group> -->

        <!-- </div> -->

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
      singleState: null,
      options: [],
      // options: [
      //   {
      //     name: ""
      //   }
      // ],
      optionsState: null
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.singleState = valid;
      this.optionsState = valid;
      return valid;
    },
    resetModal() {
      this.single = "";
      this.singleState = null;
      this.options = "";
      this.optionsState = null;
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
        label: this.single,
        options: (this.options = this.options.split(","))
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

    // addNewInput() {
    //   this.options.push({ name: "" });
    // }
  }
};
</script>
