<template>
  <div id="container">
    <div v-if="containsID">
      <v-data-table
        v-sortable-data-table
        :items="tableDataLocal"
        :headers="headers"
        :items-per-page="-1"
        item-key="Index"
        @sorted="dataTableSortOrder"
        hide-default-footer
      >
      </v-data-table>
    </div>
    <p v-else> Not All Data Contain ID</p>
  </div>
</template>

<script>
import Sortable from "sortablejs"

export default {
  name: 'ChartView',
  props: {
    tableData: [],
    tableHeaders: [],
  },
  components: {
  },
  data() {
    return {
      tableDataLocal: [],
      headers: [],
      containsID: true
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
              if(h.text != "_id" && h.text != "id")
                this.headers.push(h);
          });
        });
      }
      else
      {
        this.headers = this.tableHeaders;
      }
    },
    dataTableSortOrder(event) {
      const movedItem = this.tableDataLocal.splice(event.oldIndex, 1)[0];
      this.tableDataLocal.splice(event.newIndex, 0, movedItem);
      this.$emit('update', this.tableDataLocal)
    },
  },
  created()
  {
    this.createHeaders();
    this.tableData.forEach((item, index) => {
      item["Index"] = index;
      this.tableDataLocal.push(item);
    });
  },
  directives: {
    sortableDataTable: {
      bind(el, binding, vnode) {
        const options = {
          animation: 150,
          onUpdate: function (event) {
            vnode.child.$emit("sorted", event);
          },
        };
        Sortable.create(el.getElementsByTagName("tbody")[0], options);
      },
    },
  },
  computed:
  {
  },
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