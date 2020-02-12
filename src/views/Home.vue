<template>
  <!-- <div class="container"> -->
  <div class="row">
    <div class="col-md-6">
      <!-- <div class="container"> -->
      <AddSurvey />
      <!-- </div> -->
    </div>
    <div class="col-md-6">
      <Preview />
      <!-- </div> -->
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
    return {};
  }
};
</script>

<style lang="scss" scoped>
.col-md-6:first-child {
  min-height: 100vh;
  background-color: #f7f7f7;
}
</style>
