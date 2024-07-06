<template>
    <div class="recipe-generator">
        <br><br><br>
        <hr>
        <hr>
        <h1>您的专属菜谱:</h1>
        <hr>
        <center>
            <div class="div1">
                <p id="IBM"><b>您的BMI值为:</b> {{ nutritionData.bmi.toFixed(2) }}</p>
                <p id="rl"><b>您每日所需的热量为:</b> {{ nutritionData.tee.toFixed(2) }}</p>
                <p id="ts"><b>您每日所需的碳水化合物为:</b> {{ nutritionData.carbs.toFixed(2) }}</p>
                <p id="ss"><b>您每日所需的膳食纤维为:</b> {{ nutritionData.fiber.toFixed(2) }}</p>
                <p id="db"><b>您每日所需的蛋白质为:</b> {{ nutritionData.protein.toFixed(2) }}</p>
                <p id="zf"><b>您每日所需的脂肪为:</b> {{ nutritionData.fat.toFixed(2) }}</p>
                <p id="gc"><b>您每日所需的胆固醇为:</b> {{ nutritionData.dgc.toFixed(2) }}</p>
                <p id="ys"><b>您每日所需的叶酸为:</b> {{ nutritionData.ga.toFixed(2) }}</p>
                <p id="A"><b>您每日所需的维生素A为:</b> {{ nutritionData.va.toFixed(2) }}</p>
                <p id="B"><b>您每日所需的维生素B为:</b> {{ nutritionData.vb.toFixed(2) }}</p>
                <p id="C"><b>您每日所需的维生素C为:</b> {{ nutritionData.vc.toFixed(2) }}</p>
                <p id="D"><b>您每日所需的维生素D为:</b> {{ nutritionData.vd.toFixed(2) }}</p>
                <p id="E"><b>您每日所需的维生素E为:</b> {{ nutritionData.ve.toFixed(2) }}</p>
                <p id="Na"><b>您每日所需的钠为:</b> {{ nutritionData.na.toFixed(2) }}</p>
                <p id="K"><b>您每日所需的钾为:</b> {{ nutritionData.k.toFixed(2) }}</p>
                <p id="Ga"><b>您每日所需的钙为:</b> {{ nutritionData.ga.toFixed(2) }}</p>
                <p id="P"><b>您每日所需的磷为:</b> {{ nutritionData.p.toFixed(2) }}</p>
                <p id="Mg"><b>您每日所需的镁为:</b> {{ nutritionData.mg.toFixed(2) }}</p>
                <p id="Fe"><b>您每日所需的铁为:</b> {{ nutritionData.fe.toFixed(2) }}</p>
                <p id="Zn"><b>您每日所需的锌为:</b> {{ nutritionData.zn.toFixed(2) }}</p>
            </div>
        </center>
        <hr>
        <center>
            <div class="div2">
                <table border="1">
                    <tr>
                        <th>周一</th>
                        <th>周二</th>
                        <th>周三</th>
                        <th>周四</th>
                        <th>周五</th>
                        <th>周六</th>
                        <th>周日</th>
                    </tr>
                    <tr v-for="(meal, index) in meals" :key="index">
                        <td v-for="day in week" :key="day">{{ meal[day] }}</td>
                    </tr>
                </table>
            </div>
        </center>
        <button class="button" @click="goToLink('homepage')">返回主页</button>
        <button class="button1" @click="goToLink('input-page')">返回填写信息</button>
    </div>
</template>

<script>
export default {
    props: ['nutritionData'],
    data() {
        return {
            meals: [],
            week: ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
        };
    },
    created() {
        this.fetchOptimizedMenu();
    },
    methods: {
        fetchOptimizedMenu() {
            fetch('/optimize', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ min_weights: this.getMinWeights() }),
            })
                .then(response => response.json())
                .then(data => {
                    let breakfast = {};
                    let lunch = {};
                    let dinner = {};
                    data.forEach(dayMenu => {
                        breakfast[dayMenu.day] = dayMenu.menu[0];
                        lunch[dayMenu.day] = dayMenu.menu[1];
                        dinner[dayMenu.day] = dayMenu.menu[2];
                    });
                    this.meals = [breakfast, lunch, dinner];
                });
        },
        getMinWeights() {
            return [
                this.nutritionData.tee,
                this.nutritionData.carbs,
                this.nutritionData.fiber,
                this.nutritionData.protein,
                this.nutritionData.fat,
                this.nutritionData.dgc,
                this.nutritionData.vb9,
                this.nutritionData.va,
                this.nutritionData.vb,
                this.nutritionData.vc,
                0,  // 假设缺少 vd
                this.nutritionData.ve,
                this.nutritionData.na,
                this.nutritionData.k,
                this.nutritionData.ga,
                this.nutritionData.p,
                this.nutritionData.mg,
                this.nutritionData.fe,
                this.nutritionData.zn
            ];
        },
        goToLink(page) {
            if (page === 'homepage') {
                this.$router.push('/'); // Replace with your home route
            } else if (page === 'input-page') {
                this.$router.push('/function'); // Replace with your input form route
            }
        }
    }
}
</script>

<style scoped>
.recipe-generator {
    padding: 20px;
}

h1 {
    color: blueviolet;
    font-size: 40px;
    text-align: center;
}

img {
    width: 600px;
    position: relative;
    top: 15px;
    z-index: -1;
}

.div2 {
    color: rgb(242, 8, 8);
    font-size: 20px;
    background-color: aquamarine;
    z-index: 1;
    margin: auto;
    width: 80%;
    max-width: 800px;
    height: auto;
    border-radius: 5%;
    padding: 20px;
}

.div1 {
    background-image: url('@/assets/食物一.png'); /* Adjust the path as needed */
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    color: rgb(77, 62, 243);
    font-size: 25px;
    padding: 20px;
    border-radius: 5%;
    margin: 20px 0;
}

.button, .button1 {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
}

.button {
    position: absolute;
    top: 20px;
    left: 20px;
}

.button1 {
    position: absolute;
    top: 20px;
    right: 20px;
}

.button:hover, .button1:hover {
    background-color: #0056b3;
}
</style>