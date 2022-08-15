<script>
export default {
  name: "page-logs2",
  data() {
    this.rowsLimit = 17;
    this.tableDataBackup = null;
    return {
      sortDown: {
        log_time: false,
        user_name: false,
        log_message: false,
        log_success: false,
      },
      tableData: [],
    };
  },
  created() {
    getSimpleDBData("read_logs", "db.php", this.rowsLimit).then((data) => {
      this.tableData = data;
      this.tableDataBackup = JSON.parse(JSON.stringify(this.tableData));
    });
  },
  mounted() {
    console.log(this.$refs.refInput);
    console.log(this.$refs.refArea);
  },
  methods: {
    getCount() {
      return getSimpleDBData("get_log_count", "db.php");
    },
    // функция фильтрации вне зависимости от вводимого регистра слов
    filter(value, field) {
      if (value === "") {
        this.tableData = this.tableDataBackup;
        return;
      }
      let array = [];
      let searchArr = value.split(" ");
      for (let i = 0; i < this.tableDataBackup.length; i++) {
        const element = this.tableDataBackup[i];
        let colValue = "";
        if (field === "log_success")
          colValue = this.getSuccessName(element[field]).toLowerCase();
        else colValue = element[field].toLowerCase();
        for (let y = 0; y < searchArr.length; y++) {
          const search = searchArr[y].toLowerCase();
          if (colValue.includes(search.toLowerCase())) {
            array.push(element);
            break;
          }
        }
      }
      this.tableData = array;
    },
    // функция сброса поиска
    clear() {
      this.tableData = this.tableDataBackup;
    },
    onTextClick(e) {
      e.target.readOnly = true;
      e.target.style = '';
    },
    // функция вызова поля для поиска в любой ячейке
    onInputClick(e) {
      // let str = e.target.value;
      // let arr = str.split(/\s+/);
      // if (arr.length > 10) {
      //     e.target.style = 'height: 70px; padding-top: 4px;';
      //   }

      if (e.target.readOnly) {
        e.target.readOnly = false;
        e.target.select();
        this.$refs.refInput.style = 'none';
        this.$refs.refArea.style.display = 'block';
      }
    },
    getSuccessName(v) {
      return v ? "Успешно" : "Не успешно";
    },
    // функция сортировки всей таблицы
    sortTable(field) {
      this.sortDown[field] = !this.sortDown[field];
      const v = this.sortDown[field] ? -1 : 1;
      const v2 = this.sortDown[field] ? 1 : -1;
      this.tableData.sort(function (a, b) {
        if (a[field] > b[field]) return v;
        else if (a[field] < b[field]) return v2;
        return 0;
      });
    },
  },
};
</script>

<template>
  <div>
    <div class="d-flex p-2">
      <button class="btn-outline-primary ml-2" @click="clear">
        Сбросить поиск
      </button>
    </div>
    <div class="d-table ml-3">
      <div class="d-tr">
        <div class="d-th" @click="sortTable('log_time')" style="width: 18%">
          <div class="header-sort">
            Дата
            <v-icon
                class="svg-icon"
                v-show="tableData"
                :name="sortDown['log_time'] ? 'angle-double-down' : 'angle-double-up'"
            ></v-icon>
          </div>
        </div>
        <div class="d-th p-2" @click="sortTable('user_name')" style="width: 12%">
          <div class="header-sort">
            Пользователь
            <v-icon
                class="svg-icon"
                v-show="tableData"
                :name="sortDown['user_name'] ? 'angle-double-down' : 'angle-double-up'"
            ></v-icon>
          </div>
        </div>
        <div class="d-th" @click="sortTable('log_message')" style="width: 60%">
          <div class="header-sort">
            Сообщение
            <v-icon
                class="svg-icon"
                v-show="tableData"
                :name="sortDown['log_message'] ? 'angle-double-down' : 'angle-double-up'"
            ></v-icon>
          </div>
        </div>
        <div class="d-th" @click="sortTable('log_success')">
          <div class="header-sort">
            Результат
            <v-icon
                class="svg-icon"
                v-show="tableData"
                :name="sortDown['log_success'] ? 'angle-double-down' : 'angle-double-up'"
            ></v-icon>
          </div>
        </div>
      </div>
      <div class="d-tr" v-for="(row, index) in tableData" :key="index">
        <div class="d-td">
          <input
              :id="'searchDate' + index"
              type="text"
              class="readonly"
              :value="row.log_time"
              readonly
              @click="onInputClick($event)"
              @keydown.enter="filter($event.target.value, 'log_time')"
          />
        </div>
        <div class="d-td">
          <input
              :id="'searchUser' + index"
              type="text"
              class="readonly"
              :value="row.user_name"
              readonly
              @click="onInputClick($event)"
              @keydown.enter="filter($event.target.value, 'user_name')"
          />
        </div>
        <div class="d-td">
          <input
              :id="'searchMessage' + index"
              ref="refInput"
              type="text"
              class="readonly"
              :value="row.log_message"
              :title="row.log_message"
              readonly
              @click="onInputClick($event)"
              @blur="onTextClick($event)"
              @keydown.enter="filter($event.target.value, 'log_message')"
          />
          <textarea
              :id="'searchMessage' + index"
              ref="refArea"
              type="text"
              class="readonly"
              :value="row.log_message"
              :title="row.log_message"
              readonly
              @click="onInputClick($event)"
              @blur="onTextClick($event)"
              @keydown.enter="filter($event.target.value, 'log_message')"
          />
        </div>
        <div class="d-td">
          <input
              :id="'searchSuccess' + index"
              type="text"
              class="readonly"
              :value="getSuccessName(row.log_success)"
              readonly
              @click="onInputClick($event)"
              @keydown.enter="filter($event.target.value, 'log_success')"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.readonly {
  border: none;
  outline: 0;
  outline-offset: 0;
  cursor: pointer;
  width: 100%;
}
textarea {
  width: 100%;
  white-space: nowrap;
  text-align: center;
  overflow: hidden;
  text-overflow: ellipsis;
  resize: none;
  position: relative;
  top: 4px;
  z-index: 1;
}

textarea:focus {
  opacity: 1;
  border: none;
  outline: 2px solid #007bff;
  white-space: normal;
  overflow: visible;
  text-overflow: clip;
  width: 100%;
  padding-top: 4px;
}

input {
  width: 100%;
  text-align: center;
  position: relative;
  z-index: 0;
}

input:focus {
  text-align: center;
  opacity: 1;
  border: none;
  outline: 2px solid #007bff;
}

.d-table {
  display: table;
  width: 98%;
  border-collapse: collapse;
}

.d-tr {
  display: table-row;
}

.d-th {
  display: table-cell;
  font-weight: bold;
  border: 1px solid black;
  vertical-align: middle;
  padding: 4px;
  cursor: pointer;
  background-color: #c2c2c2;
  color: black;
}

.d-td {
  display: table-cell;
  border: 1px solid black;
  padding: 4px;
}

.header-sort {
  text-align: center;
}

.svg-icon {
  float: right;
}
</style>
