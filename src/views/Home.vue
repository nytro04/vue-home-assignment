<template>
  <div class="row">
    <div class="col-md-6">
      <AddSurvey :questions="surveyList" @updateLS="preview" />
    </div>
    <div class="col-md-6">
      <Preview :questions="surveyList" @updateLS="preview" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import AddSurvey from "../views/AddSurvey";
import Preview from "../views/Preview";

export default {
  name: "Home",
  components: {
    AddSurvey,
    Preview
  },
  data() {
    return {
      surveyList: JSON.parse(localStorage.getItem("survey"))
    };
  },
  methods: {
    preview() {
      console.log("preview");
      return (this.surveyList = JSON.parse(localStorage.getItem("survey")));
    }
  }
};
</script>

<style lang="scss" scoped>
.col-md-6:first-child {
  min-height: 100vh;
  background-color: #f7f7f7;
}
</style>
