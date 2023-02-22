<template>
  <div id="container">
     <div class="d-flex rounded" id="tableBar" v-if="tableSearch">
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
            v-for="header in headers.filter( header => header.text != 'Index')" 
            :key="headers.indexOf(header)"
          >
            <v-text-field
              v-model="item[header.text]"
              hide-details
              dense
              single-line
            ></v-text-field>
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
              headers.push(h);
          });
        });
        this.headers = headers.concat({text: "Edit", value: ""});
      }
      else
      {
        this.headers = this.tableHeaders;
        this.headers = this.headers.concat({text: "Edit", value: ""});
      }
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
</style>