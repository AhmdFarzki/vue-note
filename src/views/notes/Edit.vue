<template>
  <div class="container">
    <div class="row col-md-6">
      <div class="card">
        <div class="card-header">New Note</div>
        <div class="card-body">
          <form action="#" method="post" @submit.prevent="update">
            <div class="form-group">
              <label for="title">Title</label>
              <input
                type="text"
                v-model="form.title"
                name="title"
                id="title"
                class="form-control"
              />
              <div v-if="theErrors.title" class="mt-2 text-danger">
                {{ theErrors.title[0] }}
              </div>
            </div>
            <div class="form-group">
              <label for="subject">Subject</label>
              <select @change="selectedSubject" id="subject">
                <option :value="form.subjectId" v-text="form.subject"> </option>
                <template v-for="subject in subjects">
                  <option
                    v-if="form.subjectId !== subject.id"
                    :key="subject.id"
                    :value="subject.id"
                  >
                    {{ subject.name }}
                  </option>
                </template>
              </select>
              <div v-if="theErrors.title" class="mt-2 text-danger">
                {{ theErrors.subject[0] }}
              </div>
            </div>

            <div class="form-group">
              <label for="description">Description</label>
              <textarea
                v-model="form.description"
                id="description"
                rows="5 "
                class="form-control"
              ></textarea>
              <div v-if="theErrors.description" class="mt-2 text-danger">
                {{ theErrors.description[0] }}
              </div>
            </div>
            <button type="submit" class="btn btn-primary">
              Update
              <template v-if="loading">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  style="margin: auto; background: none; display: block; shape-rendering: auto;"
                  width="20px"
                  height="20px"
                  viewBox="0 0 100 100"
                  preserveAspectRatio="xMidYMid"
                >
                  <circle cx="84" cy="50" r="10" fill="#4658ac">
                    <animate
                      attributeName="r"
                      repeatCount="indefinite"
                      dur="0.25s"
                      calcMode="spline"
                      keyTimes="0;1"
                      values="10;0"
                      keySplines="0 0.5 0.5 1"
                      begin="0s"
                    ></animate>
                    <animate
                      attributeName="fill"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="discrete"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="#4658ac;#ff6d00;#ff003a;#e7008a;#4658ac"
                      begin="0s"
                    ></animate>
                  </circle>
                  <circle cx="16" cy="50" r="10" fill="#4658ac">
                    <animate
                      attributeName="r"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="0;0;10;10;10"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="0s"
                    ></animate>
                    <animate
                      attributeName="cx"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="16;16;16;50;84"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="0s"
                    ></animate>
                  </circle>
                  <circle cx="50" cy="50" r="10" fill="#e7008a">
                    <animate
                      attributeName="r"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="0;0;10;10;10"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.25s"
                    ></animate>
                    <animate
                      attributeName="cx"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="16;16;16;50;84"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.25s"
                    ></animate>
                  </circle>
                  <circle cx="84" cy="50" r="10" fill="#ff003a">
                    <animate
                      attributeName="r"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="0;0;10;10;10"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.5s"
                    ></animate>
                    <animate
                      attributeName="cx"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="16;16;16;50;84"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.5s"
                    ></animate>
                  </circle>
                  <circle cx="16" cy="50" r="10" fill="#ff6d00">
                    <animate
                      attributeName="r"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="0;0;10;10;10"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.75s"
                    ></animate>
                    <animate
                      attributeName="cx"
                      repeatCount="indefinite"
                      dur="1s"
                      calcMode="spline"
                      keyTimes="0;0.25;0.5;0.75;1"
                      values="16;16;16;50;84"
                      keySplines="0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1;0 0.5 0.5 1"
                      begin="-0.75s"
                    ></animate>
                  </circle>
                </svg>
              </template>
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      form: [],
      subjects: [],
      theErrors: [],
      selected: "",
      loading: false,
    };
  },
  mounted() {
    this.getSubjects();
    this.getNote();
  },

  methods: {
    async getSubjects() {
      let response = await axios.get("/api/subjects");
      if (response.status === 200) {
        this.subjects = response.data;
      }
    },

    async getNote() {
      let response = await axios.get(
        `/api/notes/${this.$route.params.noteSlug}`
      );
      this.form = response.data.data;
    },

    selectedSubject(e) {
      this.selected = e.target.value;
    },

    async update() {
      this.loading = true;

      this.form["subject"] = this.selected || this.form.subjectId;

      let response = await axios.patch(
        `/api/notes/${this.$route.params.noteSlug}/edit`,
        this.form
      );
      if (response.status == 200) {
        this.$toasted.show(response.data.message, {
          type: "success",
          duration: 3000,
        });

        this.$router.push("/notes/table");
      }
    },
  },
};
</script>
