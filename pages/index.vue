<template>
<div>
  <v-container
    ><v-row justify="center" style="margin-top: 15%">
      <v-col cols="12" sm="6" style="margin-top: 5%">
        <h3>ยินดีต้อนรับสู่</h3>
        <h1 style="color: #03a9f4; margin-top:0.5rem; margin-bottom:0.5rem">SKYCAR</h1>
        <h4>เว็บไซต์เช่ารถยนต์รายวันที่ดีที่สุดในเชียงใหม่</h4>
      </v-col>
      <v-col cols="12" sm="4">
        <h4 style="margin-bottom:0.7rem;">ให้เราพาคุณไปสู่ที่ที่คุณต้องการ</h4>
        <v-divider style="margin-bottom:0.7rem;" class="dvd" />
        <v-subtitle>ชื่อหรืออีเมลผู้ใช้</v-subtitle>
        <v-text-field
          v-model="email"
          label="E-mail"
          solo
          dense
          rounded
          :rules="emailRules"
          style="margin-top: 0.5rem"
        ></v-text-field>
        <v-list-item-subtitle>รหัสผ่าน</v-list-item-subtitle>
        <v-text-field
          v-model="password"
          :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
          :type="show2 ? 'text' : 'password'"
          :rules="[rules.required, rules.min]"
          label="Password"
          solo
          dense
          rounded
          style="margin-top: 0.5rem"
        ></v-text-field>
        <div class="text-center dvd">
          <v-btn rounded color="light-blue" style="margin-bottom: 0.5rem" dark  @click="login()"> เข้าสู่ระบบ </v-btn>
        </div>
        <v-divider style="margin-bottom:0.7rem;" class="dvd" />
        <h4>เจอเราเป็นครั้งแรก? ไม่เป็นไรสมัครสมาชิกสิ</h4>
        <div class="text-center dvd">
          <v-btn rounded color="gee" style="margin-top: 0.5rem" dark href="/register" > สมัครสมาชิก </v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</div>
        
</template>

<script>
import firebase from 'firebase/app'
import { auth } from '~/plugins/firebaseConfig.js'
export default {
  layout: 'login',
  //   layout: 'loginGoogle',
  data() {
    return {
      show2: false,
      email: '',
      password: '',
      clock: {
        el: '#clock',
        data: {
          time: '',
          date: '',
        },
      },
      emailRules: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      show1: false,
      rules: {
        required: (value) => !!value || 'Required.',
        min: (v) => v.length >= 8 || 'Min 8 characters',
      },
    }
  },
  methods: {
    checkUser() {
      var user = auth.currentUser
      console.log(user === null)
    },
    // logout() {
    //   auth
    //     .signOut()
    //     .then(() => {
    //       // Sign-out successful.
    //       console.log('Sign-out successful')
    //     })
    //     .catch((error) => {
    //       // An error happened.
    //       console.log(error)
    //     })
    // },
    login() {
      auth
        .signInWithEmailAndPassword(this.email, this.password)
        .then((result) => {
          // This gives you a Google Access Token. You can use it to access the Google API.
          const token = result.credential
          // The signed-in user info.
          const user = result.user
          console.log('token x : ' + token)
          console.log('user x : ' + user)
          alert('login successful!')
          //if (user.email == 'admin123@gmail.com') {
          //password:123123
          // console.log('admin')
          //  this.$router.replace('/admin')
          // } else if (user.email == 'owner123@gmail.com') {
          //password:123123
          //  console.log('owner')
          //  this.$router.replace('/owner')
          // } else {
          console.log('user x') //email:hamhxm@gmail.com password:123123
          this.$router.replace('/ShopEmployee')
          //loginเแบบล็อคอีเมลล์ในหน้าเดียว
        })

        .catch((error) => {
          // Handle Errors here.
          const errorCode = error.code
          const errorMessage = error.message
          console.log('ErrorCode' + errorCode)
          alert('Email or Password uncorrect!')
          console.log('ErrorCode' + errorMessage)
          // ...
        })
    },
  },
  computed: {
    index() {
      return this.$router.replace('/')
    },
  },
}
</script>
<style>
.sp {
  margin-top: 1rem;
}
.container-btn {
  width: 100%;
  display: -webkit-box;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding-top: 10px;
}
.logtitle {
  color: #333333;
  line-height: 1.2;
  text-align: center;
  width: 100%;
  display: block;
  padding-bottom: 54px;
}
.wrap-login100 {
  width: 960px;
  border-radius: 20px;
  overflow: hidden;
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 50px 50px 50px 95px;
}
.login100 {
  width: 100%;
  min-height: 100vh;
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: -webkit-linear-gradient(-135deg, #c48313, #01bcc6);
  background: -o-linear-gradient(-135deg, #ac7311, #965334);
  background: -moz-linear-gradient(-135deg, #080808, #008eab);
  background: linear-gradient(-135deg, #000000, #008eab);
}
</style>
