<template>
    <div class="container">
        <form @submit.prevent="handleSubmit" class="form1">
            <label><b>性别：</b></label>
            <input type="radio" name="gender" value="男" v-model="gender"> <b>男 </b>
            <input type="radio" name="gender" value="女" v-model="gender"> <b> 女</b>
            <br><br>

            <label for="age"><b>年龄(周岁):</b></label>
            <input type="text" id="age" placeholder="请输入年龄" v-model="age">
            <br><br>

            <label for="weight"><b>体重(kg):</b></label>
            <input type="text" id="weight" placeholder="请输入体重" v-model="weight">
            <br><br>

            <label for="height"><b>身高(m):</b></label>
            <input type="text" id="height" placeholder="请输入身高" v-model="height">
            <br><br>

            <label for="costs"><b>每周预算(元):</b></label>
            <input type="text" id="costs" placeholder="请输入预算" v-model="costs">
            <br><br>

            <label><b>忌口：</b></label>
            <input type="checkbox" value="辣椒" v-model="hobby"> <b>辣椒 </b>
            <input type="checkbox" value="海鲜" v-model="hobby"> <b>海鲜 </b>
            <input type="checkbox" value="菌类" v-model="hobby"> <b>菌类 </b>
            <input type="checkbox" value="高糖" v-model="hobby"> <b>高糖 </b>
            <input type="checkbox" value="高脂" v-model="hobby"> <b>高脂 </b>
            <br><br>

            <input type="submit" value="生成" id="submit">
        </form>

        <button id="back" @click="goToLink">返回主页</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            gender: '',
            age: '',
            weight: '',
            height: '',
            costs: '',
            hobby: []
        };
    },
    methods: {
        goToLink() {
            this.$router.push('/');
        },
        handleSubmit() {
            const payload = {
                gender: this.gender,
                age: this.age,
                weight: this.weight,
                height: this.height,
                move: "中",  // 示例数据，可以从用户输入获取
                dgc: this.hobby.includes('高脂') ? '是' : '否'
            };

            fetch('/calculate', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(payload),
            })
                .then(response => response.json())
                .then(data => {
                    this.$router.push({ name: 'result', params: { nutritionData: data } });
                });
        }
    }
}
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-image: url('@/assets/sunset-7628294_640.webp');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}

.form1 {
    background: rgba(255, 255, 255, 0.8);
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    width: 80%;
    max-width: 600px;
    margin: 20px auto;
    font-size: 18px;
    color: rgb(66, 0, 123);
}

input[type="text"], input[type="radio"], input[type="checkbox"] {
    margin: 10px 0;
}

input[type="text"] {
    width: calc(100% - 22px);
    height: 30px;
    font-size: 16px;
    padding: 2px 10px;
}

input[type="submit"] {
    width: 100%;
    height: 40px;
    font-size: 20px;
    color: rgb(221, 211, 15);
    font-weight: 800;
    background-color: rgb(133, 21, 212);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

input[type="submit"]:hover {
    background-color: rgb(153, 41, 232);
}

#back {
    margin-top: 20px;
    color: rgb(221, 211, 15);
    background: rgb(133, 21, 212);
    font-size: 20px;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

#back:hover {
    background-color: rgb(153, 41, 232);
}

button:hover {
    color: crimson;
}
</style>