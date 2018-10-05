<template>
    <div id="login-screen">
        <!--Left Side - Username/Password Input-->
        <div v-if="!loggedIn" class="split" id="login-half">
            <!--Login Fields-->
            <div id="login-fields">
                <div class="login-field" :class="usernameError ? 'input-error' : ''" style="border-bottom: 2px solid #f4ecff; border-radius: 4px 4px 0px 0px;">
                    <input id="username" placeholder="username" v-model="username">
                </div>
                <div class="login-field" :class="passwordError ? 'input-error' : ''">
                    <input id="password" type="password" placeholder="password" v-model="password">
                </div>
                <div class="login-field" @click="loginUser" id="login-button">
                    <div v-if="timeoutFlag" style="padding-top: 15px;"><icon  name="shopifyload" scale="1.5" pulse></icon></div>
                    <div v-else style="padding-top: 15px;">login</div>
                </div>
            </div>

            <!--Error Text-->
            <div v-if="usernameError" class="error-text">
                Username must be between  <br/> 8 and 24 characters
            </div>

            <div v-if="passwordError" class="error-text">
                Password must be between <br/> 8 and 24 characters
            </div>
            
            <!--Remember Me Toggle-->
            <div style="margin-top: 100px;">
                <input type="checkbox">
                <div style="float: right; margin-left: 5px;">remember me</div>
            </div>
            
            <!--Social Links-->
            <div style="margin-top: 100px; font-style: italic;">or login with</div>
            <div style="display: flex; justify-content: space-around; width: 150px; margin-top: 10px;">
                <div class="social-circle"><icon style="margin-top: 7px;" color="#7e24fa" name="brands/google"/></div>
                <div class="social-circle"><icon style="margin-top: 7px;" color="#7e24fa" name="brands/facebook"/></div>
                <div class="social-circle"><icon style="margin-top: 7px;" color="#7e24fa" name="brands/twitter"/></div>
            </div>
        </div>

        <div v-else class="split" style="background: #7e24fa; text-align: center; display: flex; flex-direction: column; justify-content: space-around; align-items: center;">
            <div style="font-weight: bold; color: white;">
                <div style="font-size: 15pt;">Congratulations</div>
                <div style="font-size: 9pt;">You have successfully logged in.</div>
            </div>

            <div id="signout-button" @click="loggedIn = !loggedIn">Sign out</div>
            <div></div>
        </div>

        <div class="split" id="logo-half">
            <div style="font-size: 15pt; font-weight: bold; margin-top: 140px; color: white;">AcmeStack</div>
            <div style="margin-top: 10px;">
                <div style="width: 60px; height: 60px; padding: 2px; background-image: linear-gradient(45deg, #7e24fa, #caaef2); border-radius: 8px;">
                    <div style="height: 90%; background: white; border-radius: 8px; padding: 2px;">
                        <div style="width: 50px; height: 50px; background: #7e24fa; border-radius: 50%; margin-left: 3px; margin-top: 2px;"></div>
                    </div>
                </div>
            </div>
        </div>
    </div> 
</template>

<script>
export default {
    data(){
        return{
            username: "",
            password: "",
            loggedIn: false,
            timeoutFlag: false,
            usernameError: false,
            passwordError: false,
        }
    },

    methods: {
        loginUser(){
            var self = this;
            this.timeoutFlag = false;

            if(!this.username.replace(/\s/g, '').length || this.username.length < 8 || this.username.length > 24){
                this.usernameError = true;
            }
            else{
                this.usernameError = false;
            }

            if(!this.password.replace(/\s/g, '').length || this.password.length < 8 || this.password.length > 24){
                this.passwordError = true;
            }
            else{
                this.passwordError = false;
            }

            if(!this.usernameError && !this.passwordError){
                this.timeoutFlag = true;
                setTimeout(function(){
                    self.timeoutFlag = false;
                    self.loggedIn = true;
                    self.username = "";
                    self.password = "";
                    console.log(self.timeoutFlag);
                }, 2000);
                // this.timeoutFlag = false;
            }
        }
    }
}
</script>

<style scoped>
.login-field input::placeholder {
  text-align: center;
  color: #caaef2;
  font-size: 12pt; 
  font-weight: bold;
}

.input-error input {
  color: #ff0051;
}

.login-field input{
  height: 100%;
  width: 100%;
  text-align: center;
  border: none;
  font-size: 12pt;
  font-weight: bold;
  color: #caaef2;
}

#login-screen{
  width: 100%;
  height: 100%;
  font-size: 12pt;
  font-weight: bold;
  color: #7e24fa;
  text-align: center;
  display: flex;
  flex-wrap: wrap-reverse;
}

.split {
  height: 100%;
  width: 300px;
  flex-grow: 1;
}

#login-half{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: #f4ecff;
}

#login-fields{
  align-self: center;
  box-shadow: 0px 3px 20px #CCC;
}

.login-field{
  width: 250px;
  height: 50px;
  background: white;
  color: #7e24fa;
  font-size: 12pt;
  font-weight: bold;
  padding: 3px;
  text-align: center;
}

#login-button{
  background: #7e24fa; 
  color: #f4ecff; 
  border-radius: 0px 0px 4px 4px;
}

#login-button:hover{
  background: #7111f8;
  cursor: pointer;
}

#signout-button{
  width: 150px; 
  padding: 5px; 
  border-radius: 20px; 
  background: white; 
  color: #7e24fa; 
  cursor: pointer;
}

#signout-button:hover{
  background: #caaef2;
  color: white;
}

.social-circle{
  border-radius: 50%;
  height: 30px;
  width: 30px;
  background: #e4d2ff;  
}

.social-circle:hover{
  background: #caaef2;
  cursor: pointer;
}

#logo-half{
  background: #7e24fa;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.error-text{
  text-align: center; 
  margin-top: 15px; 
  color: #ff0051;
}

.input-error{
  border: 2px solid #ff0051;
  padding: 1px;
}

@media only screen and (max-width: 500px) {
    #login-screen{

    }
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
}
</style>
