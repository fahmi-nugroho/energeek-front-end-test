<template>
  <body class="hold-transition register-page">
    <div class="register-box">
      <div class="register-logo">
        <img src="../assets/energeek.svg" alt="" />
      </div>
      <div class="card">
        <div class="card-body register-card-body">
          <h4 class="login-box-msg font-weight-bold text-dark">Apply Lamaran</h4>
          <form action="../../index.html" method="post">
            <div class="form-group">
              <label class="font-weight-normal text-dark">Jabatan</label>
              <select class="form-control select2" style="width: 100%">
                <option selected="selected" disabled>Pilih Jabatan</option>
                <option v-for="job in jobs" :key="job.id" :value="job.name">
                  {{ job.name }}
                </option>
              </select>
            </div>
            <label for="telepon" class="font-weight-normal text-dark">Telepon</label>
            <div class="input-group mb-3">
              <input
                id="telepon"
                type="number"
                class="form-control"
                placeholder="Cth: 0893239851289"
              />
            </div>
            <label for="email" class="font-weight-normal text-dark">Email</label>
            <div id="email" class="input-group mb-3">
              <input
                type="email"
                class="form-control"
                placeholder="Cth: energeekmail@gmail.com"
              />
            </div>
            <label for="tahun" class="font-weight-normal text-dark">Tahun Lahir</label>
            <div id="tahun" class="input-group mb-3">
              <input
                type="date"
                class="form-control"
                placeholder="Pilih tahun"
              />
            </div>
            <div class="form-group">
              <label class="font-weight-normal text-dark">Skill Set</label>
              <select
                @change="onChange"
                class="select2"
                multiple="multiple"
                data-placeholder="Select a State"
                style="width: 100%"
                placeholder="Pilih Skill"
                v-model="myskill"
              >
                <option
                  v-for="skill in skills"
                  :key="skill.id"
                  :value="skill.name"
                >
                  {{ skill.name }}
                </option>
              </select>
            </div>
          </form>
          <div class="social-auth-links text-center">
            <a @click="apply" class="btn btn-block btn-danger">
              Apply
            </a>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "login",
  data() {
    return {
      url: "http://demo73.energeek.co.id/energeek-frontend-test/public/",
      jobs: [],
      skills: [],
    };
  },
  async mounted() {
    let job = await axios.get(this.url + "api/select_list/job?search");
    let skill = await axios.get(this.url + "api/select_list/skill?search=");
    this.jobs = job.data.data.jobs;
    this.skills = skill.data.data.skills;
  },
  methods: {
    apply() {
      console.log("lallala");
      Swal.fire({
        title: "Berhasil",
        text: "Lamaran berhasil dikirim",
        icon: "success",
        confirmButtonText: "Selesai",
      });
    },
  },
};
</script>

<style>
</style>