<script>
export default {
  name: "page-logs",
  data() {
    return {
      log_message: "",
      log_date: "",
      user_name: "",
      tableDataBackup: null,
      tableData: [
        {
          log_date: "2022-03-16 10:29:30.702647",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-16 10:29:40.496121",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-16 10:42:04.513455",
          user_name: "astra",
          log_message: "Формирование отчета: Ведомость покупных изделий",
          log_success: "",
        },
        {
          log_date: "2022-03-16 10:42:19.189664",
          user_name: "astra",
          log_message: "Формирование отчета: Ведомость покупных изделий",
          log_success: "",
        },
        {
          log_date: "2022-03-16 10:42:27.712162",
          user_name: "astra",
          log_message: "Формирование отчета: Ведомость покупных изделий",
          log_success: "",
        },
        {
          log_date: "2022-03-24 14:29:05.303486",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 14:29:13.219856",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 14:42:22.478476",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 14:43:52.198631",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 15:39:21.180531",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 15:41:12.723637",
          user_name: "astra",
          log_message: "Формирование отчета: Спецификация",
          log_success: "",
        },
        {
          log_date: "2022-03-24 16:22:48.569273",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='model'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.574805",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='structure'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.576288",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='status'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.576437",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='command_center'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.577009",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='index'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.612423",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='trials'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.633152",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='trials_param_kinds'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.641646",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='group'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.647626",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='materials'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.649533",
          user_name: "gastra",
          log_message: "SELECT content from export_content where name='documents'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.695961",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='auxiliary_materials'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.702626",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='instruments'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.721347",
          user_name: "kasta",
          log_message: "SELECT content from export_content where name='riggings'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.770858",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='interfaces'",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.790858",
          user_name: "astrа",
          log_message: "SELECT product_suid from export_products where version is null",
          log_success: "t",
        },
        {
          log_date: "2022-03-24 16:22:48.801456",
          user_name: "astra",
          log_message: "SELECT content from export_content where name='eif_characteristics'",
          log_success: "t",
        },
      ],
    };
  },
  mounted() {
    this.tableDataBackup = JSON.parse(JSON.stringify(this.tableData));
  },

  methods: {
    // фильтрует по одному слову и зависит от вводимого регистра слов
    filMes(v) {
      console.log(v);
      if (v.target.value === "") {
        this.tableData = this.tableDataBackup;
        return;
      }
      let arr = [];
      for (let i = 0; i < this.tableDataBackup.length; i++) {
        const element = this.tableDataBackup[i];
        if (element.log_message.includes(this.log_message)) arr.push(element);
      }

      this.tableData = arr;
    },

    // фильтрует по одному слову вне зависимости от вводимого регистра слов
    filtMess(v) {
      if (v.target.value === "") {
        this.tableData = this.tableDataBackup;
        return;
      }
      this.tableData = this.tableDataBackup.filter((item) =>
          item.log_message.toLowerCase().includes(v.target.value.toLowerCase())
      );
    },

    // фильтрует по нескольким словам, вне зависимости от вводимого регистра слов
    filterMessage(v) {
      if (v.target.value === "") {
        this.tableData = this.tableDataBackup;
        return;
      }
      let array = [];
      let searchArr = v.target.value.split(" ");
      for (let i = 0; i < this.tableDataBackup.length; i++) {
        const element = this.tableDataBackup[i].log_message.toLowerCase();
        const elem = this.tableDataBackup[i].user_name.toLowerCase();
        const el = this.tableDataBackup[i].log_success.toLowerCase();
        for (let y = 0; y < searchArr.length; y++) {
          if (element.includes(searchArr[y].toLowerCase())) {
            array.push(this.tableDataBackup[i]);
            break;
          }
          if (elem.includes(searchArr[y].toLowerCase())) {
            array.push(this.tableDataBackup[i]);
            break;
          }
          if (el.includes(searchArr[y].toLowerCase())) {
            array.push(this.tableDataBackup[i]);
            break;
          }
        }
      }
      this.tableData = array;
    },

    // фильтрует по дате
    filterDate(v) {
      if (v.target.value === "") {
        this.tableData = this.tableDataBackup;
        return;
      }
      this.tableData = this.tableDataBackup.filter((item) =>
          item.log_date.includes(v.target.value))
    },

    // функция очистки ввода в полях поиска
    clear() {
      document.getElementById('searchDate').value = "";
      document.getElementById('searchMess').value = "";
      this.tableData = this.tableDataBackup;
    },
  }
};
</script>

<template>
  <div>
    <div class="d-flex p-2">
      <button class="btn btn-sm btn-primary mt-2 mb-1 ml-5" @click="clear">Сбросить поиск</button>
    </div>
    <div class="d-table ml-5 mb-5" style="width: 85%">
      <div class="d-tr">
        <div class="d-th" style="width: 15%; height: 50px">Дата</div>
        <div class="d-th" style="width: 10%">Пользователь</div>
        <div class="d-th" style="width: 50%">Сообщение</div>
        <div class="d-th" style="width: 15%">Результат</div>
      </div>
      <div class="d-tr">
        <div class="d-th">
          <input
              id="searchDate"
              type="date"
              style="width: 96%"
              class="form-control ml-1 mr-1 pl-5"
              v-model="log_date"
              @keydown.enter="filterDate"
          />
        </div>
        <div class="d-td" style="border-left: none; border-right: none">
          <input
              id="searchMess"
              type="text"
              style="width: 720%"
              class="form-control ml-5 mr-1 pl-5"
              placeholder="Введите для поиска пользователя/сообщения/результата"
              v-model="log_message"
              @keyup="filterMessage"
          />
        </div>
        <div class="d-td" style="border-left: none; border-right: none"></div>
        <div class="d-td" style="border-left: none"></div>

      </div>
      <div class="d-tr" v-for="(row, index) in tableData" :key="index">
        <div class="d-td">{{ row.log_date }}</div>
        <div class="d-td">{{ row.user_name }}</div>
        <div class="d-td">{{ row.log_message }}</div>
        <div class="d-td">
          <div v-if="!row.log_success">Не успешно</div>
          <div v-else>Успешно</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.d-table {
  display: table;
  width: 90%;
  border-collapse: collapse;
}
.d-tr {
  display: table-row;
}
.d-th {
  display: table-cell;
  text-align: center;
  border: 1px solid black;
  vertical-align: middle;
  padding: 4px;
}
.d-td {
  display: table-cell;
  text-align: center;
  border: 1px solid black;
  vertical-align: middle;
  padding: 4px;
}

.container {
  border: 1px solid black;
}

.row {
  text-align: center;
  vertical-align: middle;
}
</style>
