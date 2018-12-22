<template>
  <div id="app">
      <div style="margin-bottom: 30px">
        <el-switch
            style="display: block"
            v-model="editModeEnabled"
            active-color="#13ce66"
            inactive-color="#ff4949"
            active-text="Edit enabled"
            inactive-text="Edit disabled">
          </el-switch>
      </div>
       <el-table
      :data="gridData"
      style="width: 100%">
      <el-table-column
        label="Name"
        min-width="180">
        <editable-cell slot-scope="{row}"
                       :can-edit="editModeEnabled"
                       v-model="row.name">
          <span slot="content">{{row.name}}</span>
        </editable-cell>
      </el-table-column>

      <el-table-column
        min-wwidth="150"
        label="Gender">

         <editable-cell 
         slot-scope="{row}" 
         editable-component="el-select"
         :can-edit="editModeEnabled"
         close-event="change"
         v-model="row.gender">
         
          <el-tag size="medium" 
                  :type="row.gender === 'M' ? 'primary' : 'danger'" 
                  slot="content">
                  {{row.gender === 'M' ? 'Male': 'Female'}}
          </el-tag>

          <template slot="edit-component-slot">
            <el-option value="M" label="Male"></el-option>
            <el-option value="F" label="Female"></el-option>
          </template>
        </editable-cell>
        
      </el-table-column>


      <el-table-column
        label="Birth Date"
        min-width="250">
         <editable-cell 
         slot-scope="{row}" 
         :can-edit="editModeEnabled"
         editable-component="el-date-picker"
         format="yyyy-MM-dd"
         value-format="yyyy-MM-dd"
         v-model="row.date">
          <span slot="content">{{row.date}}</span>
        </editable-cell>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import EditableCell from "./components/EditableCell.vue";

export default {
  name: "App",
  components: {
    EditableCell
  },
  data() {
    return {
      editModeEnabled: false,
      gridData: [
        {
          date: "2016-05-03",
          name: "Tom",
          gender: "M"
        },
        {
          date: "2016-05-02",
          name: "Lisa",
          gender: "F"
        },
        {
          date: "2016-05-04",
          name: "Jon",
          gender: "M"
        },
        {
          date: "2016-05-01",
          name: "Mary",
          gender: "F"
        }
      ]
    };
  }
};
</script>

<style>
.edit-cell {
  min-height: 35px;
  cursor: pointer;
}
</style>
