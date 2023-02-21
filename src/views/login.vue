<template>
    <div class="container login-wrapper d-flex flex-column justify-content-center ">
        <img src="../assets/images/login-top.png" alt="tooth" class="d-md-none img-fluid d-block mx-auto mb-4" style="max-width:150px">
        <div class="col-12 col-xxl-10 mx-auto d-flex align-items-center login">
            <img src="../assets/images/login-side.png" alt="tooth" class="d-none d-md-block img-fluid">

            

            <form class="w-100 px-4 py-4 ps-xxl-4 me-md-3 pe-xxl-5" @submit.prevent>
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
                <button type="submit" class="btn btn-primary submit-btn" @click="login">Submit</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            phoneNumber: '',
            password: ''
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
            if(res.status == 'success') {
                console.log(res)
                localStorage.setItem('jwt', res.authorisation.token)
                localStorage.setItem('user', JSON.stringify(res.user))
                this.$router.push({ path: '/' })
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