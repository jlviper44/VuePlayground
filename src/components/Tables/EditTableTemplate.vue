<template>
  <div id="container">
     <div class="d-flex rounded" id="tableBar" v-if="tableSearch" >
        <v-text-field
          outlined
          hide-details
          dense
          background-color="white"
          v-model="search"
        >
        </v-text-field>
    </div>
    <v-data-table
      :items="tableDataLocal"
      :headers="headers"
      :search="search"
      :items-per-page="tableItemsPerPage"
      :hide-default-footer="tableHideDefaultFooter"
      :sort-by="tableSort"
      :sort-desc="tableSortDesc"
      :multi-sort="tableMultiSort"
    >

      <template v-slot:item="{ item }">
        <tr>
          <td 
            v-for="header in headers" 
            :key="headers.indexOf(header)"
          >
            <div v-if="header.text != 'Edit'">
              <div v-if="tableDataLocal.indexOf(item) == editCellIndex">
                <v-text-field
                  v-model="item[header.text]"
                  hide-details
                  dense
                  single-line
                ></v-text-field>
              </div>
              <div v-else>
                <span>{{item[header.text]}}</span>
              </div>
            </div>
            <div v-else>
              <div v-if="
                  editCellIndex == tableDataLocal.indexOf(item)
                "
                class="editButton"
              >
                <v-icon
                  color="error"
                  @click="
                    cancelButtonClicked()
                  "
                  class="editButton"
                >
                  mdi-window-close
                </v-icon>
                <v-icon
                  class="editButton"
                  color="success"
                  @click="
                    saveButtonClicked()
                  "
                >
                  mdi-content-save
                </v-icon>
              </div>
              <div v-else class="editButtonDiv">
                <center>
                  <v-icon
                    class="editButton"
                    color="success"
                    @click="
                      editButtonClicked(item)
                    "
                  >
                    mdi-pencil
                  </v-icon>
                  <v-icon
                    class="editButton"
                    color="error"
                    
                  >
                    mdi-delete
                  </v-icon>
                </center>
              </div>
            </div>
          </td>
        </tr>
      </template>
    </v-data-table>
  </div>
</template>

<script>

export default {
  name: 'ChartView',
  props: {
    tableData: [],
    tableHeaders: [],
    tableItemsPerPage: Number,
    tableHideDefaultFooter: Boolean,
    tableMultiSort: Boolean,
    tableSearch: Boolean
  },
  components: {
  },
  data() {
    return {
      search: "",
      headers: [],
      tableSort: [],
      tableSortDesc: [],
      tableDataLocal: [],
      defaultCell: {},
      editCellIndex: null
    }
  },
  methods:
  {
    createHeaders()
    {
      if(this.tableHeaders == undefined && this.tableData != 0)
      {
        let headers = [];
        this.tableData.forEach((data) => {
          Object.keys(data).forEach((header) => {
            let h = {
              text: header,
              value: header
            };
            if(!headers.some(header => header.text == h.text))
              if(h.text != "Index")
                headers.push(h);
          });
        });
        this.headers = headers.concat({text: "Edit", value: "", width: "5%", align: "center"});
      }
      else
      {
        this.headers = this.tableHeaders;
        this.headers = this.headers.concat({text: "Edit", value: "", width: "5%", align: "center"});
      }
      this.headers.forEach((header) => {
        if(header.text != "Edit")
          header["width"] = (100 / this.headers.length - 10).toString() + "%"
      });
    },
    editButtonClicked(item)
    {
      if(this.editCellIndex == this.tableDataLocal.indexOf(item))
      {
        this.editCellIndex = null;
        this.defaultCell = {};
      }
      else
      {
        this.editCellIndex = this.tableDataLocal.indexOf(item);
        this.defaultCell = Object.assign({}, item);
      }
    },
    cancelButtonClicked()
    {
      for (const [key] of Object.entries(this.tableDataLocal[this.editCellIndex])) {
        this.tableDataLocal[this.editCellIndex][key] = this.defaultCell[key]; 
      }
      this.defaultCell = {};
      this.editCellIndex = null;
    },
    saveButtonClicked()
    {
      this.editCellIndex = null;
      this.defaultCell = {};
      this.$emit('update', this.tableDataLocal);
    }
  },
  created()
  {
    this.createHeaders();
    this.tableData.forEach((item, index) => {
      item["Index"] = index;
      this.tableDataLocal.push(item);
    });
  }
}
</script>
<style scoped>
#container {
  padding: 10px;
  margin: 10px;
}
#tableBar {
  padding: 10px;
  background-color: lightblue;
  margin-bottom: 5px;
}
.editButton {
  padding: 5px;
}
.editButtonDiv {
  margin-left: -15px;
  /* margin: auto; */
  /* padding: 5px; */
  /* align-content: left; */
}
</style>