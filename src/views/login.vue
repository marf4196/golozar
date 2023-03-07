<template>
    <div class="container login-wrapper d-flex flex-column justify-content-center ">
        <img src="../assets/images/login-top.png" alt="tooth" class="d-md-none img-fluid d-block mx-auto mb-4" style="max-width:150px">
        <div class="col-12 col-xxl-10 mx-auto d-flex align-items-center login">
            <img src="../assets/images/login-side.png" alt="tooth" class="d-none d-md-block img-fluid">
            
            <form class="w-100 px-4 py-4 ps-xxl-4 me-md-3 pe-xxl-5" @submit.prevent>
                <div class="alert alert-danger d-flex align-items-center mt-3 mb-4" role="alert" v-if="loginFailed">
                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" fill="currentColor" class="bi bi-exclamation-triangle-fill flex-shrink-0 me-2" viewBox="0 0 16 16" role="img" aria-label="Warning:">
                        <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
                    </svg>
                    <div class="pt-1 ps-2">
                        Login failed, Please try again.
                    </div>
                </div>
                <h2 class="mb-4 fw-bolder">LOGIN TO CONTINUE</h2>
                <div class="mb-3 mt-3">
                    <label for="phone" class="form-label fw-semibold">Phone Number:</label>
                    <input type="tel" minlength="10" maxLength="10" required pattern="[0-9]{10}" v-model="phoneNumber" class="form-control py-2"  id="phone" placeholder="Enter phone number" name="phone">
                    <small>Example: 912*******</small>
                </div>
                <div class="mb-3 py-2">
                    <label for="pwd" class="form-label fw-semibold">Password:</label>
                    <input type="password" minlength="1" required v-model="password" class="form-control py-2" id="pwd" placeholder="Enter password" name="pswd">
                </div>
                <div class="form-check mb-3 py-2">
                    <label class="form-check-label fw-semibold">
                    <input class="form-check-input" type="checkbox" name="remember"> Remember me
                    </label>
                </div>
                <button type="submit" class="btn btn-primary submit-btn" @click="login">
                    Submit
                    <div class="spinner-border spinner-border-sm ms-2" role="status" v-if="showSpinner"></div>
                </button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            phoneNumber: '',
            password: '',
            loginFailed: false,
            showSpinner: false,
        }
    },
    methods: {
        async login() {
            let body = {
                phone: this.phoneNumber,
                password: this.password
            }
            let res = await fetch('http://194.5.212.149/api/auth/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(body),
            })
            res = await res.json()
            console.log(res)
            if(res && res.status == 'success') {
                console.log(res)
                localStorage.setItem('jwt', res.authorisation.token)
                localStorage.setItem('user', JSON.stringify(res.user))
                this.$router.push({ path: '/' })
            }
            else {
                this.loginFailed = true;
            }
        }
    }
}
</script>

<style>
    body {
        background-color: #F7F9FB;
    }
    
    .login-wrapper {
        height: 100vh;
    }

    .login {
        background-color: #fff;
        box-shadow: 0px 0px 10px rgb(0 0 0 / 10%);
    }

    .login label {
        font-size: 14px;
    }

    .login .submit-btn {
        background-color: #0dabef;
        border-color: #0dabef;
        padding: 8px 24px;
        font-weight: 500;
        width: 100%;
    }

    .login form h2 {
        color: #5d5d5d;
    }

    @media screen and (max-width: 768px) {
        .login {
            border-radius: 8px;
        }
    }
</style>