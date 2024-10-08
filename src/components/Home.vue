<script>
import About from './About.vue'
import Methods from './Methods.vue'
import Contact from './Contact.vue'

export default {
    components: {
        About,
        Methods,
        Contact
    },
    data() {
        return {
            currentPage: 'about'
        }
    },
    methods: {
        sendDataToParent(page) {
        },
    }
}

</script>

<template>
    <nav id="navbar" dir="rtl">
        <div class="navitem">
            <button class="navbtn" @click="this.currentPage = 'about'">
                درباره دکتر علوی
            </button>
        </div>
        <div class="navitem" @click="this.currentPage = 'methods'">
            <button class="navbtn">
                روش های درمان
            </button>
        </div>
        <div class="navitem">
            <button class="navbtn" @click="this.currentPage = 'contact'">
                ارتباط با دکتر
            </button>
        </div>
        <div class="navitem">
            <button class="navbtn" @click="this.$emit('update-data', 'request')">
                درخواست نوبت
            </button>
        </div>
        <div class="navitem">
            <button class="navbtn" v-on:click="this.$emit('update-data', 'login')">
                ورود
            </button>
        </div>
    </nav>
    <div>
        <Transition>
            <About v-if="this.currentPage == 'about'"></About>

        </Transition>
        <Transition>
            <Methods v-if="this.currentPage == 'methods'"></Methods>

        </Transition>
        <Transition>
            <Contact v-if="this.currentPage == 'contact'"></Contact>

        </Transition>
    </div>
</template>

<style>
body {
    margin: 15px 0px;
}

#navbar {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.navitem {
    align-self: center;
    margin: 5px 20px;
}

.navbtn {
    width: 150px;
    padding: 15px;
    background-color: #2ecc71;
    text-decoration: none;
    border: 0;
    border-radius: 3px;
    cursor: pointer;
}
</style>