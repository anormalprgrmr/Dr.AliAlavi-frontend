<script>
export default {
    data() {
        return {

        }
    }
}
</script>

<template>
    <div style="display:inline; width: 700px;">
        <h1 style="padding: 50px;text-align: center;">درخواست نوبت</h1>
        <div style="display: flex ;justify-content: center;">
            <table dir="rtl">
                <tr>
                    <td>نام :</td>
                    <td><input type="text"></td>
                </tr>
                <tr>
                    <td>نام خانوادگی :</td>
                    <td><input type="text"></td>
                </tr>
                <tr>
                    <td>سابقه بیماری :</td>
                    <td><textarea style="width: 95%;" type="text"></textarea></td>
                </tr>
                <tr>
                    <td>تاریخ :</td>
                    <td><input type="text"></td>
                </tr>
                <tr>
                    <td>ساعت :</td>
                    <td><input type="text"></td>
                </tr>
                <tr></tr>
            </table>
        </div>
        <div style="text-align: center;">

            <div>
                <button>ارسال</button>
            </div>

            <div>
                <button @click="this.$emit('update-data','homenpm')">بازگشت</button>
            </div>

        </div>

    </div>

</template>

<style>
.lbl {
    position: relative;
    right: 0;
}

.inp {
    text-align: left;
}

.sec {
    /* text-align: center; */
    padding: 15px;
}
</style>