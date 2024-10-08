<script>
export default {
    data() {
        return {
            datas: []
        }
    },
    beforeMount() {
        this.getDataFromAPI()
    },
    methods: {
        async getDataFromAPI() {
            const token = localStorage.getItem('myToken')

            const url = "http://localhost:8081/admin/data";
            try {
                const response = await fetch(url, { method: "GET", headers: { 'Authorization': 'Bearer ' + token } });
                if (!response.ok) {
                    throw new Error(`Response status: ${response.status}`);
                }

                const json = await response.json();
                this.datas = json
                console.log(this.datas);
            } catch (error) {
                console.error(error.message);
            }


        },
        async changeStatus(id, newStatus) {
            const token = localStorage.getItem('myToken')

            const url = "http://localhost:8081/admin/change-status";
            try {
                const response = await fetch(url, {
                    method: "POST",
                    body: JSON.stringify({ id: id, status: newStatus }),
                    headers: {
                        'Authorization': 'Bearer ' + token,
                        'Content-Type': "application/json"
                    }
                });
                if (!response.ok) {
                    throw new Error(`Response status: ${response.status}`);
                }

                const json = await response.json();
                this.getDataFromAPI()
                console.log(this.datas);
            } catch (error) {
                console.error(error.message);
            }
        }
    }
}

</script>

<template>
    <h1 style="text-align: center;">Admin Panel</h1>

    <table id="table" dir="rtl" border="1">
        <tr>
            <th>نام</th>
            <th>نام خانوادگی</th>
            <th>شماره تلفن</th>
            <th>تاریخ</th>
            <th>ساعت</th>
            <th>سابقه بیماری</th>
            <th>وضعیت</th>
            <th>تغییر وضعیت</th>
        </tr>

        <tr v-for="data in this.datas">
            <td>{{ data.firstname }}</td>
            <td>{{ data.lastname }}</td>
            <td>{{ data.phonenumber }}</td>
            <td>{{ data.date }}</td>
            <td>{{ data.time }}</td>
            <td>{{ data.description }}</td>
            <td>{{ data.status }}</td>
            <td dir="rtl">
                <button @click="changeStatus(data.id, 'قبول شده')">قبول</button>
                <button @click="changeStatus(data.id, 'رد شده')">رد کردن</button>
            </td>
        </tr>

    </table>
    <button v-on:click="this.$emit('update-data','home')">Home Page</button>

</template>

<style>
.row {}

#table {
    border-collapse: collapse;
    margin: 5px auto;
}

th {
    font-size: 16px;
    font-family: bold;
    padding: 9px;
}

td {
    padding: 9px;
}
</style>