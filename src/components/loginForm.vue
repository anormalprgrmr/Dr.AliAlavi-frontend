<script>

export default {
    props: {
        txt: String
    },
    data() {
        return {
            statusLogin: 'status *********',
            msg: 'Hello',
            username: '',
            password: '',
            myresponse: 'nothing',
            token: localStorage.getItem('myToken')
        }
    },
    computed: {
        token(newToken) {
            return newToken.token
        }
    }
    ,
    methods: {
        sendDataToParent(page) {
            this.$emit('update-data',page); // Emit event to parent
        },
        async login(username, password) {
            const myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/json");
            const url = "http://localhost:8081/get-token";
            try {
                const response = await fetch(url, {
                    method: 'POST',
                    body: JSON.stringify({ username: username, password: password }),
                    headers: myHeaders
                })

                if (!response.ok) {
                    throw new Error(`Response status: ${response.status}`);
                }


                this.sendDataToParent('admin')
                const json = await response.json();
                this.statusLogin = 'admin'
                localStorage.setItem('myToken', json.token)
            } catch (error) {
                console.error(error.message);
            }

        },
    }

}
</script>

<template>
    <div class="userinput">
        <input name="username" type="text" id="usernamefield" v-model="username">
        <label for="username" style="margin-left: 25px ;">: نام کاربری</label>
    </div>

    <div style="display: flex;flex-wrap: wrap;flex-direction: row;justify-content: center;">
        <input name="password" type="text" id="passwordfield" v-model="password"
            style="position: relative; left: -4px;">
        <label for="password" style="margin-left: 25px ;">: رمز عبور</label>
    </div>

    <button id="btnlogin" v-on:click.prevent="
    
    try {
        login(username, password)
    } catch (error) {
        console.log(error);
    }

        " >ورود</button>

    <button id="btnhome" v-on:click.prevent="this.$emit('update-data','home');" >
        صفحه اصلی
    </button>

</template>

<style>
.userinput {
    display: flex;
    justify-content: center;
    margin-bottom: 40px;
}

body {
    background-color: #ecf0f1;
    margin-top: 135px;
}

#btnlogin {
    display: block;
    text-align: center;
    margin: 45px auto 15px auto;
    position: relative;
    left: -10px;
    width: 200px;
    padding: 15px 10px;
    background-color: #2ecc71;
    border: 0px;
    border-radius: 6px;
}
#btnhome {
    display: block;
    text-align: center;
    margin: 0px auto;
    position: relative;
    left: -10px;
    width: 200px;
    padding: 15px 10px;
    background-color: #95a5a6;
    border: 0px;
    border-radius: 6px;
}
</style>