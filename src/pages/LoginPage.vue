<script>
import {loginUrl, getHeader, userUrl} from './../config'
export default {
  data () {
    return {
      login: {
        email: 'yandikurniawan@gmail.com',
        password: '123456'
      }
    }
  },
  methods: {
    handleLoginFormSubmit () {
      const postData = {
        grant_type: 'password',
        client_id: '2',
        client_secret: 'FCRCvhO9rtXyOUTQBO4kGvRUIFkVj0KmvvBkx7Ay',
        username: this.login.email,
        password: this.login.password,
        scope: ''
      }
      const authUser = {}
      this.$http.post(loginUrl, postData).then(response => {
        if (response.status === 200) {
          console.log(response)
          authUser.access_token = response.data.access_token
          authUser.refresh_token = response.data.refresh_token
          window.localStorage.setItem('authUser', JSON.stringify(authUser))
          this.$http.get(userUrl, {headers: getHeader()}).then(response => {
            console.log(response)
            authUser.email = response.body.email
            authUser.name = response.body.name
            window.localStorage.setItem('authUser', JSON.stringify(authUser))
            this.$router.push({name: 'dashboard'})
          })
        }
      })
    }
  }
}
</script>

<template>
  <div class="wrapper" id="login-wrapper">
    <section class="login">
        <div class="row">
            <div class="col-md-6 col-md-push-3">
                <div class="panel panel-default">
                    <div class="panel-heading"><strong>Login</strong></div>
                    <div class="panel-body">
                        <form v-on:submit.prevent="handleLoginFormSubmit()">
                            <div class="form-group">
                                <label>E-mail</label>
                                <input class="form-control" placeholder="E-mail" type="text" v-model="login.email">
                            </div>
                            <div class="form-group">
                                <label>Password</label>
                                <input class="form-control" placeholder="Password" type="password" v-model="login.password">
                            </div>
                            <button class="btn btn-primary">Login</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </section>
  </div>

</template>

<style>
#login-wrapper{
margin-top: 150px;
}
</style>
