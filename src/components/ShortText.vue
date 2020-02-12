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

    <b-modal id="modal-prevent-closing" ref="short-modal" title="Short Text" @show="resetModal" @hidden="resetModal" @ok="handleOk">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group :state="shortState" label="Please enter your short survey question" label-for="short-input" invalid-feedback="Short input is required">
          <b-form-input id="short-input" v-model="short" :state="shortState" required></b-form-input>
        </b-form-group>
      </form>
      <template v-slot:modal-footer="{ ok, cancel }">
        <!-- Emulate built in modal footer ok and cancel button actions -->
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
      short: "",
      shortState: null,
      submittedNames: []
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.shortState = valid;
      return valid;
    },
    resetModal() {
      this.short = "";
      this.shortState = null;
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

      console.log(this.short);

      const shortSurvey = {
        type: "SHORT TEXT",
        name: this.short
      };

      console.log(shortSurvey);

      localStorage.setItem(
        "survey",
        JSON.stringify([...surveyDB, shortSurvey])
      );

      console.log(JSON.parse(localStorage.getItem("survey")));

      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("modal-prevent-closing");
      });
    }
  }
};
</script>
