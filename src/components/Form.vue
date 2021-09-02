<template>
  <form id="signup-form" @submit.prevent="submitRegister">
    <div class="row py-4">
      <div class="col-6 form-group pb-2">
        <label
          for="fullname"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Full Name <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="text"
            class="form-control"
            v-model="fullName"
            id="fullname"
            autocomplete="off"
          />

          <div
            v-if="fullNameError"
            class="error-message d-flex text-danger fs-6"
          >
            {{ fullNameError }}
          </div>
        </div>
      </div>

      <div class="col-6 form-group pb-2">
        <label
          for="phone"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Phone <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="number"
            class="form-control"
            v-model="phone"
            id="phone"
            autocomplete="off"
          />

          <div v-if="phoneError" class="error-message d-flex text-danger fs-6">
            {{ phoneError }}
          </div>
        </div>
      </div>

      <div class="col-12 form-group pb-2">
        <label
          for="email"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Email <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="email"
            class="form-control"
            v-model="email"
            id="email"
            autocomplete="off"
          />
          <div v-if="emailError" class="error-message d-flex text-danger fs-6">
            {{ emailError }}
          </div>
        </div>
      </div>

      <div class="col-12 form-group pb-2">
        <label
          for="country"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Country <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <select
            name=""
            id="country"
            class="form-control"
            autocomplete="off"
            v-model="country"
          >
            <option value="germany">Germany</option>
            <option value="canada">Canada</option>
            <option value="nigeria">Nigeria</option>
          </select>
          <div
            v-if="countryError"
            class="error-message d-flex text-danger fs-6"
          >
            {{ countryError }}
          </div>
        </div>
      </div>

      <div class="col-6 form-group pb-2">
        <label
          for="password"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Password <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="password"
            class="form-control"
            v-model="password"
            id="password"
            autocomplete="off"
          />
          <div
            v-if="passwordError"
            class="error-message d-flex text-danger fs-6"
          >
            {{ passwordError }}
          </div>
        </div>
      </div>

      <div class="col-6 form-group pb-2">
        <label
          for="cpassword"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Confirm Password <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="password"
            class="form-control"
            v-model="confirmPassword"
            id="cpassword"
            autocomplete="off"
          />
          <div
            v-if="confirmPasswordError"
            class="error-message d-flex text-danger fs-6"
          >
            {{ confirmPasswordError }}
          </div>
        </div>
      </div>

      <div class="col-12 form-group pb-2">
        <label
          for="skills"
          class="col-form-label col-form-label-md d-flex fw-bold"
          >Skills (add 7 programming skills with space key after each skill)
          <span class="text-danger">&nbsp;*</span></label
        >
        <div>
          <input
            type="text"
            class="form-control"
            v-model="tempSkill"
            id="skills"
            autocomplete="off"
            @keyup.space="addSkills"
          />
          <div v-if="skillsError" class="error-message d-flex text-danger fs-6">
            {{ skillsError }}
          </div>
          <div class="d-flex">
            <p
              v-for="(skill, i) in skills"
              :key="skill"
              class="pill px-3 py-1 rounded-pill mt-2 fw-bold"
            >
              <span>
                {{ skills[i] }} &nbsp;
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-x-circle text-danger"
                  viewBox="0 0 16 16"
                  @click="deleteSkill(skill)"
                >
                  <path
                    d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"
                  />
                  <path
                    d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"
                  />
                </svg>
              </span>
            </p>
          </div>
        </div>
      </div>

      <div class="col-12 form-group pb-2">
        <div class="form-check">
          <input
            type="checkbox"
            class="form-check-input"
            id="check"
            v-model="terms"
          />
          <label
            for="check"
            class="terms-condition form-check-label d-flex text-secondary fw-bold"
            >Accept our terms and condition</label
          >
          <div v-if="termsError" class="error-message d-flex text-danger fs-6">
            {{ termsError }}
          </div>
        </div>
      </div>

      <div class="col-12 form-group d-flex py-2">
        <button class="btn btn-submit" ref="createBtn">Create account</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "Form",

  data() {
    return {
      fullName: "",
      email: "",
      phone: "",
      country: "",
      password: "",
      confirmPassword: "",
      tempSkill: "",
      skills: [],
      terms: false,
      passwordError: "",
      fullNameError: "",
      emailError: "",
      phoneError: "",
      countryError: "",
      confirmPasswordError: "",
      skillsError: "",
      termsError: "",
    };
  },

  methods: {
    submitRegister() {
      this.fullNameError = this.fullName ? "" : "full name is required";
      this.phoneError = this.phone ? "" : "phone is required";
      this.countryError = this.country ? "" : "Please select your country";
      this.confirmPasswordError =
        this.password === this.confirmPassword ? "" : "passwords not match";

      if (!this.password) {
        this.passwordError = "password is required";
      } else if (this.password <= 4) {
        this.passwordError = "password should be at least 5 characters";
      }

      if (!this.email) {
        this.emailError = "email address is required";
      } else if (
        !/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
          String(this.email).toLowerCase()
        )
      ) {
        this.emailError = "Invalid email address";
      }

      alert('Form submitted')

      this.resetFields();
    },

    resetFields() {
      this.fullName = "";
      this.email = "";
      this.phone = "";
      this.country = "";
      this.password = "";
      this.confirmPassword = "";
      this.skills = [];
      this.terms = false;
    },

    addSkills(e) {
      if (e.key === " " && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          if (this.skills.length + 1 <= 7) {
            this.skills.push(this.tempSkill);
          } else if (e.key === " " && !this.tempSkill) {
            this.tempSkill = "";
            return this.skills;
          }
        }
        this.tempSkill = "";
      } else {
        return this.skills;
      }
    },

    deleteSkill(skill) {
      this.skills = this.skills.filter((el) => {
        return skill !== el;
      });
    },
  },
};
</script>

<style>
.btn-submit {
  background-color: #31344f;
  color: #fff;
}

.btn-submit:hover {
  background-color: #31344fb8;
  color: #fff;
}

/* .error-message {
  font-size: 12px;
  color: red;
} */

.pill {
  background-color: #eee;
  display: inline-flex;
  margin-right: 5px;
  font-size: 14px;
}

svg {
  cursor: pointer;
}
</style>
