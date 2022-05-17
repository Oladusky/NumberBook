<template>
  <div class="cardModal" v-if="visible">
    <div>Добавление пользователя</div>
    <div class="modalClose" v-on:click="closeModal()">&#10006;</div>
    <div class="modalOption">
      <div>Имя</div>
      <input v-model="name" type="text" />
    </div>
    <div class="modalOption">
      <div>Телефон</div>
      <input v-model="number" type="text" />
    </div>
    <div class="modalOption">
      <div>Начальник</div>
      <select v-model="boss">
        <option v-for="(option, id) in personInfo" :key="id">
          {{ option.name }}
        </option>
      </select>
    </div>
    <div>
      <button @click="saveData">Сохранить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      name: '',
      number: '',
      boss: '',
      visible: false,
      personInfo: [],
      key: '',
    };
  },
  mounted() {
    if (localStorage.getItem("data") !== null) {
      this.personInfo = JSON.parse(localStorage.getItem("data"));
    }
  },
  methods: {
    closeModal() {
      this.visible = false;
      this.name = '';
      this.number = '';
      this.boss = '';
    },
    saveData() {
      this.personInfo.push({
        name: this.name,
        number: this.number,
        boss: this.boss,
      });
      let json = JSON.stringify(this.personInfo);
      localStorage.setItem("data", json);
      this.$parent.saveData();
    },
  },
};
</script>

<style scoped>
.modalOption {
  display: flex;
  justify-content: space-between;
  margin: auto;
}

.modalOption {
  display: flex;
  justify-content: space-between;
  margin: 10px 30px 10px 0;
}

.modalOption div {
  margin: 0 30px 0 0;
}

.cardModal {
  width: 300px;
  height: 150px;
  border-radius: 20px;
  border: 1px black solid;
  margin: auto;
  position: relative;
  text-align: left;
  padding: 10px 10px;
}

.modalClose {
  position: absolute;
  margin: 5px 10px 0 0;
  top: 0;
  right: 0;
}

.modalTitle {
  margin: 10px 0 10px 10px;
}

.modalDescription {
  margin: 10px 10px 0 10px;
}
</style>
