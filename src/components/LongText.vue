<template>
  <div>
    <b-modal id="long-survey-text" ref="long-modal" title="Long Text" @show="resetModal" @hidden="resetModal" @ok="handleOk">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group :state="longState" label="Please enter your long survey question" label-for="long-input" invalid-feedback="Long input is required">
          <b-form-textarea id="long-input" v-model="long" placeholder="Enter your long question..." rows="3" max-rows="6" :state="longState" required></b-form-textarea>
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
      long: "",
      longState: null
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.longState = valid;
      return valid;
    },
    resetModal() {
      this.long = "";
      this.longState = null;
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

      let surveyDB = JSON.parse(localStorage.getItem("survey"));
      surveyDB = surveyDB ? surveyDB : [];

      const longSurvey = {
        name: "LONG TEXT",
        label: this.long
      };

      localStorage.setItem("survey", JSON.stringify([...surveyDB, longSurvey]));

      this.$emit("reload");

      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("long-survey-text");
      });
    }
  }
};
</script>
