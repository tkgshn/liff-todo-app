<template>
    <div>
        <h1> Todo create</h1>
        <b-container fluid>
            <b-form  v-if="show">
                <b-col sm="3">
                    <label>ToDo:</label>
                </b-col>
                <b-col sm="5" style="padding-bottom: 30px">
                    <b-form-input type="text" v-model="form.subject" placeholder="ToDoを入力してください"></b-form-input>
                </b-col>
                <b-col sm="3">
                    <label for="datepicker">期限：</label>
                </b-col>
                <b-col sm="5" style="padding-bottom: 30px">
                    <b-form-datepicker id="datepicker" v-model="form.limit" class="mb-2" ></b-form-datepicker>
                </b-col>
            </b-form>
            <b-button style="margin: 10px" type="submit" variant="primary" @click="todoRegister()">Submit</b-button>
        </b-container>
    </div>
</template>
<script>
import liff from "@line/liff";
import axios from "axios";
export default {
    name: 'CreateToDo',
    data() {
        return {
            form: {
                subject: '',
                limit: ''
                },
                show: true
            }
    },
    created() {
        liff.init(
            {
                liffId: process.env.VUE_APP_LIFF_ID,
            }
        )
    },
    methods: {
        async todoRegister(){
            const token = await liff.getAccessToken();
            try{
                const res = await axios.post(
                    process.env.VUE_APP_REGISTER_API,{
                        params:{
                            channel_id: process.env.VUE_APP_LINE_CHANNEL_ID,
                            access_token: token,
                            subject: this.form.subject,
                            limit: this.form.limit
                        },
                        headers: {
                            'Content-Type': 'application/json'
                        }
                    }
                )
                console.log("API Called");
                console.log(res.data);
                this.final_message = "成功しました";
                alert(this.final_message);
                liff.closeWindow();
            }catch(error){
                if (error.response) {
                this.final_message = `ステータスコード: ${error.response.status}`;
                //リクエストを実行し,サーバーからレスポンスがない場合
                } else {
                    this.final_message = "リクエストに失敗しました。";
                }
                alert(this.final_message);
                liff.closeWindow();
            }
        }
    }
}
</script>
<style scoped>
.todo-form {
    padding-bottom: 30px;
}
</style>