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

    <b-modal
      id="single-choice-survey"
      ref="single-choice"
      title="Single Choice"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          :state="nameState"
          label="Please enter your single choice survey question"
          label-for="single-choice"
          invalid-feedback="input is required"
        >
          <b-form-input
            id="single-choice"
            v-model="single"
            :state="nameState"
            required
          ></b-form-input>
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
      single: ""
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
      this.nameState = valid;
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
      // Push the name to submitted names
      this.submittedNames.push(this.long);
      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("single-choice-survey");
      });
    }
  }
};
</script>
