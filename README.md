# vite_vue3_bmi
vite_安裝vue3製作BMI元件
透過Vite來建立一個Vue 3的BMI指數計算器元件非常簡單，只要跟著以下步驟就可以完成：

### 0. 安裝 Node.js

在開始之前，你需要確保已經安裝了Node.js。請前往 [Node.js官方網站](https://nodejs.org/) 下載並安裝適合你作業系統的版本。安裝完成後，你可以在終端機（命令提示字元）中輸入以下指令來確認Node.js和npm（Node.js的套件管理器）已經被正確安裝：

```bash
node -v
npm -v
```

這會顯示出Node.js和npm的版本號，確認你已經安裝好這些工具。

### 1. 安裝 Vite

有了Node.js環境之後，打開終端機（命令提示字元），然後使用下面的指令來創建一個新的Vite + Vue 3專案：

```bash
npm create vite@latest 你的專案名稱 --template vue
```

將 `你的專案名稱` 替換為你想要的專案名字，例如：`bmi-calculator`。

### 2. 安裝專案依賴

切換到你的專案目錄：

```bash
cd 你的專案名稱
```

然後安裝專案依賴：

```bash
npm install
```

### 3. 創建 BMI 指數元件

在 `src/components` 資料夾內創建一個名為 `BmiCalculator.vue` 的檔案，並加入以下內容：

```vue
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
      <div v-if="bmi" class="result">
        <p>你的 BMI 是：{{ bmi }}</p>
        <p v-if="bmi < 18.5">建議：體重過輕，應適當增加營養攝入。</p>
        <p v-else-if="bmi >= 18.5 && bmi < 24">建議：體重適中，請保持良好的生活方式。</p>
        <p v-else-if="bmi >= 24 && bmi < 27">建議：體重過重，應適當控制飲食並適量運動。</p>
        <p v-else-if="bmi >= 27 && bmi < 30">建議：屬於輕度肥胖，應積極控制飲食並養成運動習慣。</p>
        <p v-else-if="bmi >= 30 && bmi < 35">建議：屬於中度肥胖，應嚴格控制飲食並持續運動。</p>
        <p v-else>建議：屬於重度肥胖，

應立即尋求專業指導並採取必要措施。</p>
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
        bmi.value = (weight.value / (heightInMeters ** 2)).toFixed(2)
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
```

### 4. 在主頁面使用 BMI 元件

打開 `src/App.vue` 檔案，引入並使用你的 `BmiCalculator` 元件：

```vue
<script setup>

import BMI from './components/Bmi.vue'


</script>

<template>
  <BMI/>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

```

### 5. 運行專案

回到終端機，運行以下指令啟動你的專案：

```bash
npm run dev
```

現在，你的瀏覽器應該會自動打開 `localhost:5173`，並且展示你的BMI計算器了！

以上就是使用Vite來建立一個Vue 3的BMI指數計算器的完整教學，希望這對你有所幫助！