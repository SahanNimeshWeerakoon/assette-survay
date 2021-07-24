<template>
  <div class="home">
    <div class="table-border border">
      <b-row class="align-center">
        <b-col md="9" class="border-bottom">
          <b-row>
            <b-col cols="8" class="text-center justify-members"><b>{{ selected.length }} Members Selected</b></b-col>
            <b-col cols="4" class="text-center justify-members">
              <b-dropdown id="dropdown-right" text="Filter By All" variant="outline-primary" v-model="filterOn" class="m-2 mr-2 filterStatus">
                <b-dropdown-item @click="changeFilterOn('')" :active="filterOn==''">All</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('1 reminder sent')" :active="filterOn=='1 reminder sent'">1 reminder sent</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Survey Started')" :active="filterOn=='Survey Started'">Survey Started</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Survey sent')" :active="filterOn=='Survey sent'">Survey sent</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Survey completed')" :active="filterOn=='Survey completed'">Survey completed</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('2 reminders sent')" :active="filterOn=='2 reminders sent'">2 reminders sent</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Invitation sent')" :active="filterOn=='Invitation sent'">Invitation sent</b-dropdown-item>
                <template v-slot:button-content>
                  <img alt="Drop Down Icon" src="../assets/dropdownIcon.png" />
                  <span class="d-none d-md-inline-block">&nbsp;{{filterOn !== '' ? filterOn : 'Filter By All'}}</span>
                </template>
              </b-dropdown>
            </b-col>
          </b-row>
        </b-col>
        <b-col md="3" class="text-center justify-members border-bottom searchDiv">
          <div class="has-search">
            <span class="fa fa-search form-control-feedback"></span>
            <input type="text" v-model="filter" class="form-control" placeholder="Search">
          </div>
        </b-col>
      </b-row>
      
      <!-- Desktop table -->
      <b-table
          :items="filteredMembers"
          :filter="filter"
          :fields="fields"
          ref="selectableTable"
          selectable
          @row-selected="onRowSelected"
          responsive="md"
          class="d-none d-sm-block d-sm-none d-md-block"
        >

        <template v-slot:head(selected)="data">
          <input type="checkbox" @change="selectAll($event)" />
        </template>
      
        <template #cell(selected)="data">
          <span :id="data.item.id"></span>
          <input type="checkbox" :id="`checkbox${data.item.id}`" :checked="data.rowSelected" @change="onCheck(data.item.id)" />
        </template>

        <template #cell(actions)="data">
          <button class="faBtn">
            <i class="fa fa-pencil-square-o" aria-hidden="true"></i>
          </button>
          <button class="faBtn">
            <i class="fa fa-trash-o" aria-hidden="true"></i>
          </button>
        </template>

      </b-table>
      <!-- mobile table -->
      <b-table
          :items="filteredMembers"
          :filter="filter"
          :select-mode="mode"
          :fields="mobileFields"
          ref="selectableTablemobile"
          selectable
          @row-selected="onRowSelected"
          responsive="md"
          class="d-md-none"
        >

        <template #cell(plus)="row">
          <button class="btn-invisible">
            <i class="fa fa-chevron-right" v-if="!row.detailsShowing" @click="row.toggleDetails" aria-hidden="true"></i>
            <i class="fa fa-chevron-down" v-if="row.detailsShowing" @click="row.toggleDetails" area-hidden="true"></i>
          </button>
        </template>

        <template #row-details="row">
          <b-card>
            <b-row class="mb-2">
              <b-col cols="5">LANGUAGE</b-col>
              <b-col cols="7">{{ row.item.language }}</b-col>
            </b-row>
            <b-row class="mb-2">
              <b-col cols="5">EMAIL</b-col>
              <b-col cols="7">{{ row.item.email }}</b-col>
            </b-row>
            <b-row class="mb-2">
              <b-col cols="5">ATTRIBUTE 1</b-col>
              <b-col cols="7">{{ row.item.attr1 }}</b-col>
            </b-row>
            <b-row class="mb-2">
              <b-col cols="5">ATTRIBUTE 2</b-col>
              <b-col cols="7">{{ row.item.attr2 }}</b-col>
            </b-row>
            <b-row class="mb-2">
              <b-col cols="5">STATUS</b-col>
              <b-col cols="7">{{ row.item.status }}</b-col>
            </b-row>
          </b-card>
        </template>

        <template #cell(actions)="data">
          <b-dropdown id="dropdown-right" style="" text="Filter By All" variant="outline-primary" v-model="filterOn" class="m-2 mr-2 actionDropdown">
            <b-dropdown-item>Edit</b-dropdown-item>
            <b-dropdown-item>Delete</b-dropdown-item>
            <template v-slot:button-content>
              <i class="fa fa-ellipsis-v" aria-hidden="true"></i>
            </template>
          </b-dropdown>
        </template>

        <template v-slot:head(selected)="data">
          <input type="checkbox" @change="selectAll($event)" />
        </template>

        <template #cell(selected)="data">
          <span :id="`mobile${data.item.id}`"></span>
          <input type="checkbox" :id="`checkbox${data.item.id}`" :checked="data.rowSelected" @change="onCheck(data.item.id)" />
        </template>

      </b-table>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data() {
    return {
      filter: "",
      filterOn: "",
      sortBy: "",
      mode: 'multi',
      selected: [],
      mobileFields: [
        { key: 'plus', label: '', sortable: false},
        { key: 'selected', label: '<p>test</p>', sortable: false, sortDirection: 'desc'},
        { key: 'id', label: 'ID', sortable: true, sortDirection: 'desc'},
        { key: 'name', label: 'Name', sortable: false},
        { key: 'actions', label: '', sortable: false}
      ],
      fields: [
        { key: 'selected', label: '<p>test</p>', sortable: false, sortDirection: 'desc'},
        { key: 'id', label: 'ID', sortable: true, sortDirection: 'desc'},
        { key: 'name', label: 'Name', sortable: false},
        { key: 'language', label: 'LANGUAGE ', sortable: false},
        { key: 'email', label: 'EMAIL', sortable: false},
        { key: 'attr1', label: 'ATTRIBUTE 1', sortable: false},
        { key: 'attr2', label: 'ATTRIBUTE 2', sortable: false},
        { key: 'status', label: 'STATUS', sortable: false},
        { key: 'actions', label: '', sortable: false}
      ],
      members: [],
      filteredMembers: []
    };
  },
  created() {
    this.members = [
        {
          id: 73411,
          name: 'Bradley Steele',
          language: 'English',
          email: 'runalfsdottir.cindy@gmail.com',
          attr1: 'Team 1',
          attr2: 'Senior',
          status: '1 reminder sent',
          selected: true
        },
        {
          id: 63686,
          name: 'Rosa Davis',
          language: 'English',
          email: 'hester.grady@ada.ca',
          attr1: 'Team 2',
          attr2: 'Senior',
          status: 'Survey sent',
          selected: true
        },
        {
          id: 72970,
          name: 'Rosa Johnson',
          language: 'English',
          email: 'jana.ondricka@hegmann.biz',
          attr1: 'Team 3',
          attr2: 'Senior',
          status: 'Survey Started',
          selected: false
        },
        {
          id: 53589,
          name: 'florence Dixon',
          language: 'English',
          email: 'padberg_korbin@yahoo.com.cindy@gmail.com',
          attr1: 'Team 1',
          attr2: 'Senior',
          status: 'Survey completed',
          selected: false
        },
        {
          id: 62457,
          name: 'Viola Diaz',
          language: 'English',
          email: 'reinger_lydia@gmail.com',
          attr1: 'Team 1',
          attr2: 'Junior',
          status: '2 reminders sent',
          selected: false
        },
        {
          id: 24025,
          name: 'Victor Wills',
          language: 'English',
          email: 'chesley.kunde@elien.io',
          attr1: 'Team 2',
          attr2: 'Junior',
          status: 'Invitation sent',
          selected: false
        },
        {
          id: 88081,
          name: 'Clarence Garner',
          language: 'English',
          email: 'lisandro.lindgren@hotmail.com',
          attr1: 'Team 3',
          attr2: 'Junior',
          status: 'Invitation sent',
          selected: false
        }
      ];
    this.filteredMembers = [...this.members]
  },
  components: {
    HelloWorld
  },
  methods: {
    onRowSelected(items) {
      this.selected = items
    },
    onCheck(id) {
      document.getElementById(id).click();
      document.getElementById(`mobile${id}`).click();
    },
    selectAll(event) {
      let checked = event.target.checked;
      if(checked) {
        this.$refs.selectableTable.selectAllRows();
        this.$refs.selectableTablemobile.selectAllRows();
      } else {
        this.$refs.selectableTable.clearSelected();
        this.$refs.selectableTablemobile.clearSelected();
      }
    },
    changeFilterOn(val) {
      this.filterOn = val;
      let filtMem;
      if(val!=="") {
        filtMem = this.members.filter(member => member.status == val);
      } else {
        filtMem = this.members.filter(member => true);
      }
      this.filteredMembers = [...filtMem];
    }
  }
}
</script>

<style lang="scss">
.home {
  padding: 40px 30px;
  .table-border {
    border-radius: 10px;
    overflow: hidden;
    .justify-members {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      padding-left: 30px;
    }
  }
  .filterStatus {
    margin-right: 0 !important;
    margin-left: auto !important;
    @media screen and (max-width: 700px) {
      margin-right: 10px !important;
    }
  }
  .searchDiv {
    @media screen and (max-width: 700px) {
      padding-top: 10px;
      padding-bottom: 10px;
    }
    .has-search {
      width: 98%;
      margin-right: 2%;
      margin-left: auto;
      .form-control {
          padding-left: 2.375rem;
      }
      .form-control-feedback {
          position: absolute;
          z-index: 2;
          display: block;
          width: 2.375rem;
          height: 2.375rem;
          line-height: 2.375rem;
          text-align: center;
          pointer-events: none;
          color: #aaa;
      }
    }
  }
  .selected {
    border: 1px solid #3366FF;
    margin-bottom: -1px;
    background: #EFF3FF;
  }
  .faBtn {
    background: none;
    border: none;
    padding: 5px;
    i {
      font-size: 1.25em;
    }
  }
  .btn-invisible {
    background: transparent;
    border: none;
  }
  .d-md-inline-block {
    @media screen and (min-width: 700px) {
      display: inline-block !important;
    }
  }
  .table.b-table > tbody > .table-active, .table.b-table > tbody > .table-active > th, .table.b-table > tbody > .table-active > td {
    background: #EFF3FF !important;
    border-top: 1px solid #3366FF !important;
    border-bottom: 1px solid #3366FF !important;
    position: relative;
    z-index: 10;
    &:first-child {
      border-left: 1px solid #3366FF !important;
    }
    &:last-child {
      border-right: 1px solid #3366FF !important;
    }
  }
  .actionDropdown {
    margin: 0 !important;
    padding: 0 !important;
    button {
      border: none;
      color: #000;
      padding: 0;
      margin: 0;
      &:hover {
        background: transparent;
      }
      &:focus {
        outline: none;
      }
      &:active {
        background: transparent;
      }
    }
  }
  .btn-outline-primary:not(:disabled):not(.disabled).active, .btn-outline-primary:not(:disabled):not(.disabled):active, .show>.btn-outline-primary.dropdown-toggle {
    background: transparent;
    color: #000;
    &:focus {
      outline: none;
    }
  }
.table.b-table > thead > tr > [aria-sort=ascending], .table.b-table > tfoot > tr > [aria-sort=ascending],
.table.b-table > thead > tr > [aria-sort=descending], .table.b-table > tfoot > tr > [aria-sort=descending],
.table.b-table > thead > tr > [aria-sort=none], .table.b-table > tfoot > tr > [aria-sort=none] {
  width: 20px;
  background-image: url("../assets/idIcon.png");
  
}
}
</style>