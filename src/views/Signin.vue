<template>
  <div class="login-container">
    <div class="tab-content">
      <div class="login-child-container">
        <h1 class="login-title">Welcome Back!</h1>
        <div class="login-input-field">
          <input
            placeholder=" "
            type="text"
            maxlength="88"
            autocomplete="off"
            class="login-input"
            v-model="email"
          >
          <label class="login-label">Username</label>
        </div>
        <div class="login-input-field">
          <input
            placeholder=" "
            type="password"
            maxlength="100000"
            autocomplete="off"
            class="login-input"
            v-model="password"
          >
          <label class="login-label">Password</label>
        </div>
        <p class="forgot">
          <a class="login-link">Forgot Password?</a>
        </p>
        <p>
          <v-btn class="login-link" to="/join">
            <b>Not a member?</b>
          </v-btn>
        </p>
        <button class="login-button" v-on:click="login">Log In</button>
        <span class="status">{{status}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "signin",
  components: {},
  data: function() {
    return {
      email: "",
      password: "",
      status: ""
    };
  },
  methods: {
    login() {
      var oData = {
        userName: this.email,
        password: this.password
      };

      if (this.email === "" || this.password === "") {
        this.status = "Please fill in your login details";
      } else {
        this.$store
          .dispatch("login", oData)
          .then(res => {
            this.$store.commit("setAuthenticated", true);
            this.$router.push("dashboard");
          })
          .catch(error => {
            alert(error);
          });
      }
    }
  }
};
</script>

<style>
.login-container {
  background: rgba(0, 0, 0, 0.8);
  border-radius: 2px;
  box-shadow: 0 0 0 5px rgba(0, 0, 0, 0.8);
  padding: 40px;
  max-width: 600px;
  display: flex;
  height: 100%;
  position: fixed;
  justify-content: center;
  width: 100%;
  left: 50%;
  transform: translateX(-50%);
}

.tab-content {
  min-height: 420px;
  padding: 50px 0;
}

.login-child-container {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  width: 75%;
}

.login-title {
  text-align: center;
  color: #ffffff;
  font-weight: 300;
  margin: 0 0 40px;
  font-size: 32px;
  box-sizing: border-box;
}

.login-input-field {
  position: relative;
  margin-bottom: 40px;
}

.login-label {
  position: absolute;
  transform: translateY(6px);
  left: 3px;
  color: rgba(255, 255, 255, 0.5);
  transition: all 0.25s ease;
  pointer-events: none;
  font-size: 22px;
  top: 3px;
}

.required-star {
  margin: 2px;
  color: #0566ad;
}

.login-input {
  font-size: 22px;
  display: block;
  width: 100%;
  height: 100%;
  padding: 10px 10px 2px 10px;
  background: none;
  border: 1px solid #a0b3b0;
  color: #ffffff;
  border-radius: 0;
  -webkit-transition: border-color 0.25s ease, -webkit-box-shadow 0.25s ease;
  transition: border-color 0.25s ease, -webkit-box-shadow 0.25s ease;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
  transition: border-color 0.25s ease, box-shadow 0.25s ease,
    -webkit-box-shadow 0.25s ease;
  margin-left: -10px;
  border-top: 0 !important;
  border-left: 0 !important;
  border-right: 0 !important;
}

.login-input:focus {
  border-top: 0;
  border-left: 0;
  border-right: 0;
  outline: 0 !important;
}

.login-input:focus + .login-label,
.login-input:not(:placeholder-shown) + .login-label {
  top: -15px;
  font-size: 12px;
}

.forgot {
  margin-top: -30px;
  text-align: right;
}

.login-button {
  width: 100%;
  border: 0;
  outline: auto;
  outline-color: #0566ad;
  border-radius: 0;
  padding: 15px 0;
  font-size: 2rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  background: black;
  color: #ffffff;
  -webkit-transition: all 0.5s ease;
  transition: all 0.5s ease;
  -webkit-appearance: none;
  cursor: pointer;
}

.login-button:hover {
  background: #005bb3;
}

.login-link {
  color: #179b77 !important;
  border: 0;
  outline: 0;
  text-decoration: none;
  font-weight: bold;
  background: unset !important;
  -webkit-box-shadow: unset !important;
  box-shadow: unset !important;
}

.status {
  color: white;
  text-align: center;
  position: absolute;
  bottom: -70px;
  width: 270px;
  left: 50%;
  transform: translateX(-50%);
}
</style>