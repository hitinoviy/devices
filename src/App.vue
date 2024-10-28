<template>
  <div className="main">
    <h1 className="main__title">Устройства</h1>
    <div className="main__wrapper">
      <input className="main__input" type="text" v-model="deviceName" placeholder="Название устройства">
      <input className="main__input" type="text" v-model="deviceNodesSting" placeholder="Название узлов через запятую">
      <button className="main__btn" @click="sendData">Добавить устройство</button>
    </div>
    
    <p class="error" v-if="error">{{ error }}</p>
    <deviceItems 
      v-for="(el, i) in devices" 
      :key="i" 
      :info="el" 
      :index="i" 
      :deleteDevice="deleteDevice" 
      :insertData="insertData"
    />
  </div>
</template>

<script>
import deviceItems from './components/deviceItems.vue';

export default {
  components: {
    deviceItems
  },
  data() {
    return {
      devices: [],
      deviceName: '',
      deviceNodesSting: '',
      error: ''
    }
  },
  methods: {
    sendData() {
      // Проверка на пустые значения
      if (!this.deviceName) {
        this.error = 'Имя устройства не введено';
        return;
      }
      
      if (!this.deviceNodesSting) {
        this.error = 'Узлы не введены';
        return;
      }
      
      // Сброс ошибки
      this.error = '';

      // Разделение строки узлов с удалением лишних пробелов
      const deviceNodes = this.deviceNodesSting.split(',').map(node => node.trim());

      // Добавление нового устройства
      this.devices.push({
        name: this.deviceName,
        nodes: deviceNodes
      });

      // Очистка полей ввода
      this.deviceName = '';
      this.deviceNodesSting = '';
    },
    deleteDevice(index) {
      this.devices.splice(index, 1);
    }
  }
}
</script>


<style scoped src="/src/assets/style/app.css">
</style>