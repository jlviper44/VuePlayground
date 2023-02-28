<template>
  <div>
    <div class="tableDiv">
      <h2>Basic Table</h2>
      <table-template 
        :tableData="tableData"
      />
    </div>
    <div class="tableDiv">
      <h2>Draggable Table</h2>
      <draggable-table-template
        :tableData="dragableTableData" @update="val => { dragableTableData = val }"
      />
    </div>
    <div class="tableDiv">
      <h2>Edit Table</h2>
      <edit-table-template 
        :tableData="tableData" @update="val => { tableData = val }"
      />
    </div>
  </div>
</template>

<script>
import TableTemplate from '@/components/Tables/TableTemplate.vue'
import DraggableTableTemplate from '@/components/Tables/DraggableTableTemplate.vue'
import EditTableTemplate from '@/components/Tables/EditTableTemplate.vue'

export default {
  name: 'TableView',
  components: { TableTemplate, DraggableTableTemplate, EditTableTemplate },
  data() {
    return {
      tableData: [
        {
          "name": "Adkins Keller",
          "gender": "male",
          "company": "VIASIA",
          "email": "adkinskeller@viasia.com",
          "phone": "+1 (898) 460-2200"
        },
        {
          "name": "Cameron Manning",
          "gender": "male",
          "company": "VERBUS",
          "email": "cameronmanning@verbus.com",
          "phone": "+1 (803) 422-3956"
        },
        {
          "name": "Rich Sn_ider",
          "gender": "male",
          "company": "DYNO",
          "email": "richsn_ider@dyno.com",
          "phone": "+1 (929) 546-3686"
        },
        {
          "name": "Flora Rose",
          "gender": "female",
          "company": "GEEKETRON",
          "email": "florarose@geeketron.com",
          "phone": "+1 (976) 480-2493"
        },
        {
          "name": "Beverly Jenkins",
          "gender": "female",
          "company": "NEWCUBE",
          "email": "beverlyjenkins@newcube.com",
          "phone": "+1 (927) 464-3798"
        },
        {
          "name": "Lavonne Gay",
          "gender": "female",
          "company": "DATACATOR",
          "email": "lavonnegay@datacator.com",
          "phone": "+1 (891) 579-2438"
        },
        {
          "name": "Adkins Keller",
          "gender": "male",
          "company": "VIASIA",
          "email": "adkinskeller@viasia.com",
          "phone": "+1 (898) 460-2200"
        },
        {
          "name": "Cameron Manning",
          "gender": "male",
          "company": "VERBUS",
          "email": "cameronmanning@verbus.com",
          "phone": "+1 (803) 422-3956"
        },
        {
          "name": "Rich Sn_ider",
          "gender": "male",
          "company": "DYNO",
          "email": "richsn_ider@dyno.com",
          "phone": "+1 (929) 546-3686"
        },
        {
          "name": "Flora Rose",
          "gender": "female",
          "company": "GEEKETRON",
          "email": "florarose@geeketron.com",
          "phone": "+1 (976) 480-2493"
        },
        {
          "name": "Beverly Jenkins",
          "gender": "female",
          "company": "NEWCUBE",
          "email": "beverlyjenkins@newcube.com",
          "phone": "+1 (927) 464-3798"
        },
        {
          "name": "Lavonne Gay",
          "gender": "female",
          "company": "DATACATOR",
          "email": "lavonnegay@datacator.com",
          "phone": "+1 (891) 579-2438"
        }
      ],
      dragableTableData: [
        {
          "_id": "63f5201ac70be74917c1d83b",
          "name": "Blake Brady",
          "gender": "male",
          "company": "SURETECH",
          "email": "blakebrady@suretech.com",
          "phone": "+1 (963) 429-3317"
        },
        {
          "_id": "63f5201aa8e3ed2a89bc7948",
          "name": "Lily Levine",
          "gender": "female",
          "company": "GRACKER",
          "email": "lilylevine@gracker.com",
          "phone": "+1 (901) 422-3213"
        },
        {
          "_id": "63f5201a53405fb935faea95",
          "name": "Marylou Valdez",
          "gender": "female",
          "company": "SAVVY",
          "email": "marylouvaldez@savvy.com",
          "phone": "+1 (851) 453-3794",
        },
        {
          "_id": "63f5201a98e70bae81bb7bdb",
          "name": "Marsh Hahn",
          "gender": "male",
          "company": "UNISURE",
          "email": "marshhahn@unisure.com",
          "phone": "+1 (972) 600-2813"
        },
        {
          "_id": "63f5201a1e74840ac160df8b",
          "name": "Black Luna",
          "gender": "male",
          "company": "DIGIPRINT",
          "email": "blackluna@digiprint.com",
          "phone": "+1 (820) 581-2923"
        },
        {
          "_id": "63f5201ab099878bb58a3d67",
          "name": "Cook Hoover",
          "gender": "male",
          "company": "PHOTOBIN",
          "email": "cookhoover@photobin.com",
          "phone": "+1 (925) 412-3666"
        }
      ],
    }
  },
  methods:
  {
  },
  created()
  {
  },
  watch: {
  }
}
</script>
<style scoped>
.tableDiv
{
  margin: 10px;
}
</style>