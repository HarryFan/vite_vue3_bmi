<template>
    <div class="container">
      <h2>BMI 指數計算器</h2>
      <div class="input-group">
        <label for="height">身高（cm）:</label>
        <input v-model="height" type="number" id="height" />
      </div>
      <div class="input-group">
        <label for="weight">體重（kg）:</label>
        <input v-model="weight" type="number" id="weight" />
      </div>
      <div class="btn-group">
        <button class="btn" @click="calculateBMI">計算 BMI</button>
        <button class="btn" @click="resetFields">重設</button>
      </div>
      <div v-if="bmi !== null" class="result">
        <p v-if="!isNaN(bmi) && !(height === 0 && weight === 0)">你的 BMI 是：{{ bmi }}</p>
        <p v-else-if="height === 0 && weight === 0">請輸入有效的身高和體重。</p>
        <p v-else>發生錯誤，請檢查輸入值。</p>
        <p v-if="bmi < 18.5">建議：體重過輕，應適當增加營養攝入。</p>
        <p v-else-if="bmi >= 18.5 && bmi < 24">建議：體重適中，請保持良好的生活方式。</p>
        <p v-else-if="bmi >= 24 && bmi < 27">建議：體重過重，應適當控制飲食並適量運動。</p>
        <p v-else-if="bmi >= 27 && bmi < 30">建議：屬於輕度肥胖，應積極控制飲食並養成運動習慣。</p>
        <p v-else-if="bmi >= 30 && bmi < 35">建議：屬於中度肥胖，應嚴格控制飲食並持續運動。</p>
        <p v-else>建議：屬於重度肥胖，應立即尋求專業指導並採取必要措施。</p>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    setup() {
      const height = ref(0)
      const weight = ref(0)
      const bmi = ref(null)
  
      const calculateBMI = () => {
        const heightInMeters = height.value / 100
        const result = weight.value / (heightInMeters ** 2)
        bmi.value = isNaN(result) ? null : result.toFixed(2)
      }
  
      const resetFields = () => {
        height.value = 0
        weight.value = 0
        bmi.value = null
      }
  
      return {
        height,
        weight,
        bmi,
        calculateBMI,
        resetFields
      }
    }
  }
  </script>
  
 
  <style>
.container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.input-group {
  margin-bottom: 10px;
}

label {
  display: inline-block;
  width: 80px;
  font-weight: bold;
}

input[type="number"] {
  padding: 5px;
  border-radius: 3px;
  border: 1px solid #ccc;
}

.btn-group {
  margin-top: 10px;
}

.btn {
  padding: 8px 16px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  margin-right: 10px;
}

.btn:hover {
  background-color: #45a049;
}

.result {
  margin-top: 20px;
  font-weight: bold;
}
  </style>