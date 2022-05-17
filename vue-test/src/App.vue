<template>
  <div id="app" class="">
    <table>
      <tr class="head">
        <th>
          Имя:
          <select>
            <option @click="sortParam = 'first'">А-Я</option>
            <option @click="sortParam = 'second'">Я-А</option>
          </select>
        </th>
        <th>Телефон:</th>
        <th>Начальник:</th>
      </tr>
      <tr class="rows" v-for="(item, id) in  sortedItems || tableInfo" :key="id">
        <th class="rows_elem">{{ item.name }}</th>
        <th class="rows_elem">{{ item.number }}</th>
        <th class="rows_elem">{{ item.boss }}</th>
      </tr>
    </table>
    <button @click="openModal">Добавить</button>
    <button @click="clearLocal">Очистить</button>
    <Form ref="modal" />
  </div>
</template>


<script>
import Form from "./components/Form.vue";

export default {
  data() {
    return {
      sortParam: '',
      tableInfo: [],
      visible: true,
    };
  },
  created() {
    this.saveData();
  },
  computed: {
    sortedItems() {
      switch (this.sortParam) {
        case "first":
          return this.tableInfo.sort((a, b) => a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1);
        case "second":
          return this.tableInfo.sort((a, b) => b.name.toLowerCase() > a.name.toLowerCase()  ? 1  : -1);
        default:
          return this.name;
      }
    },
  },
  name: "App",
  components: {
    Form,
  },
  methods: {
    openModal: function () {
      this.$refs.modal.visible = true;
    },
    saveData: function () {
      this.tableInfo = JSON.parse(localStorage.getItem("data"));
    },
    clearLocal: function () {
      localStorage.removeItem("data");
      this.saveData();
      this.$refs.modal.personInfo = [];
    },
  },
};
</script>

<style>
table {
  width: 50%;
  border-collapse: collapse;
  margin: auto;
}
.head {
  color: #ffffff;
  font-weight: bold;
  background: #00bf80;
}
.rows {
  border: 1px solid #01ab73;
}
.rows_elem {
  border: 1px solid #e8e9eb;
}
.rows:nth-child(even) {
  background: #f4f4f4;
}
.rows:hover {
  background: #ebffe8;
}
button {
  display: block;
  margin: 10px auto;
  font-weight: 700;
  color: white;
  text-decoration: none;
  padding: 5px;
  border-radius: 8px;
  background: rgb(64, 199, 129);
  transition: 0.2s;
}
button:hover {
  background: rgb(53, 167, 110);
}
button:active {
  background: rgb(33, 147, 90);
  box-shadow: 0 3px rgb(33, 147, 90) inset;
}
</style>
