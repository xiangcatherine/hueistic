<template>
  <div class="container">
    <h2>change password</h2>
    <form class="form">
      <div class="fieldset">
        <label class="change-password" for="old-password">old</label>
        <input
          class="change-password-input"
          type="password"
          id="old-password"
          v-model="old" />
      </div>
  
      <div class="fieldset">
        <label class="change-password" for="new-password">new</label>
        <input
          class="change-password-input"
          id="new-password"
          type="password"
          v-model="password" />
        <span class="error-message"></span>
      </div>
  
      <div class="fieldset">
        <button @click.prevent="changePassword()">do it</button>
      </div>
    </form>
  
    <div class="error-message"></div>
  </div>
</template>

<script>
  export default {
    name: 'ChangePassword',
    data: function () {
      return {
        old: '',
        password: ''
      }
    },
    methods: {
      closeModal: function () {
        $('.modal').css('display', 'none')
      },
      changePassword: function () {
        var vm = this

        vm.$store
          .dispatch(
            'changePassword', {old: this.old, new: this.password}
          )
          .then(
            function () {
              vm.$toaster.success('password updated')
            }
          )
          .catch(
            function () {
              vm.$toaster.error("password couldn't be updated")
            }
          )
      }
    }
  }
</script>

<style scoped>
  .container {
    display: inline-block;
    border: 1px solid gray;
    padding: 2rem;
    background: #b0d4a2
  }

  h2 {
    font-weight: bold;
    padding-bottom: .75rem;
  }

  .fieldset {
    margin-top: 1rem;
  }

  label {
    display: block;
  }

  .fieldset > * {
    margin-bottom: .5rem;
  }

  .change-password-input {
    padding: .5rem;
    border: 1px solid gray;
  }

  .change-password-input:hover,
  .change-password-input:focus {
    outline: 0;
    border-color: black;
  }

  .error-message {
    display: none;
  }
</style>
