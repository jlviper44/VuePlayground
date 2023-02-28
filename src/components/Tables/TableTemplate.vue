<template>
  <div id="container">
    <div class="d-flex rounded" id="tableBar" v-if="tableSearch" 
      :style="{'background-color':tableSearchColor}"
    >
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
      :items="tableData"
      :headers="headers"
      :search="search"
      :items-per-page="tableItemsPerPage"
      :hide-default-footer="tableHideDefaultFooter"
      :sort-by="tableSort"
      :sort-desc="tableSortDesc"
      :multi-sort="tableMultiSort"
    >
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
    tableSearch: Boolean,
    tableSearchColor: String
  },
  components: {
  },
  data() {
    return {
      search: "",
      headers: [],
      tableSort: [],
      tableSortDesc: [],
      color: "blue"
    }
  },
  methods:
  {
    createHeaders()
    {
      if(this.tableHeaders == undefined && this.tableData != 0)
      {
        this.tableData.forEach((data) => {
          Object.keys(data).forEach((header) => {
            let h = {
              text: header,
              value: header
            };
            if(!this.headers.some(header => header.text == h.text))
              this.headers.push(h);
          });
        });
      }
      else
      {
        this.headers = this.tableHeaders;
      }
    }
  },
  created()
  {
    this.createHeaders();
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
  margin-bottom: 5px;
}
</style>