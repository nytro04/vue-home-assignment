<template>
  <div>
    <!-- <b-button v-b-modal.modal-prevent-closing>Open Modal</b-button> -->

    <!-- <div class="mt-3">
      Submitted Names:
      <div v-if="submittedNames.length === 0">--</div>
      <ul v-else class="mb-0 pl-3">
        <li v-for="name in submittedNames" :key="name">{{ name }}</li>
      </ul>
    </div> -->

    <b-modal id="single-choice-survey" ref="single-choice" title="Single Choice" @show="resetModal" @hidden="resetModal" @ok="handleOk">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group :state="singleState" label="Please enter your single choice survey question" label-for="single-choice" invalid-feedback="input is required">
          <b-form-input id="single-choice" v-model="single" :state="nameState" required></b-form-input>
          <!-- <b-form-radio-group
            id="single-choice"
            v-model="selected"
            :options="options"
            buttons
            button-variant="outline-dark"
            stacked
            name="radio-btn-stacked"
            :state="longState"
            required
          ></b-form-radio-group> -->
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
      //   selected: "",
      //   options: [
      //     { text: "Yes", value: "Yes" },
      //     { text: "No", value: "No" }
      //   ]
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
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return;
      }
      // Push the name to submitted names

      let surveyDB = JSON.parse(localStorage.getItem("survey"));
      surveyDB = surveyDB ? surveyDB : [];

      console.log(this.single);

      localStorage.setItem(
        "survey",
        JSON.stringify([...surveyDB, this.single])
      );

      console.log(JSON.parse(localStorage.getItem("survey")));

      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("single-choice-survey");
      });
    }
  }
};
</script>
