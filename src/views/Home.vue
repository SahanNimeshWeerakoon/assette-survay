<template>
  <div class="home">
    <div class="table-border border">
      <b-row class="align-center">
        <b-col cols="2" class="text-center justify-members"><b>2 Members Selected</b></b-col>
        <b-col cols="6" class="text-center"></b-col>
        <b-col cols="4" class="text-center justify-members">
          <b-row class="justify-members">
            <b-col cols="5" class="text-center justify-members">
              <b-dropdown id="dropdown-right" text="Filter By All" variant="outline-primary" v-model="filterOn" class="m-md-2">
                <b-dropdown-item @click="changeFilterOn('')" :active="filterOn==''">All</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('1 reminder sent')" :active="filterOn=='1 reminder sent'">1 reminder sent</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Started')" :active="filterOn=='Started'">Started</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('Completed')" :active="filterOn=='Completed'">Completed</b-dropdown-item>
                <b-dropdown-item @click="changeFilterOn('2 reminders sent')" :active="filterOn=='2 reminders sent'">2 reminders sent</b-dropdown-item>
                <template v-slot:button-content>
                  <img alt="Drop Down Icon" src="../assets/dropdownIcon.png" />
                  {{filterOn !== '' ? filterOn : 'Filter By All'}}
                </template>
              </b-dropdown>
            </b-col>
            <b-col cols="7" class="text-center mt-md-2 mb-md-2 justify-members">
              <div class="has-search">
                <span class="fa fa-search form-control-feedback"></span>
                <input type="text" v-model="filter" class="form-control" placeholder="Search">
              </div>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
      <b-table
          :items="members"
          :filter="filter"
          :select-mode="mode"
          :fields="fields"
          :filter-included-fields="[filterOn]"
          ref="selectableTable"
          selectable
          @row-selected="onRowSelected"
          @row-clicked="handleClick"
          responsive="sm"
        >
          <template #cell(selected)="data">
            <template v-if="data.rowSelected">
              <span :id="data.item.id"></span>
              <input type="checkbox" :id="`checkbox${data.item.id}`" checked @change="onCheck(data.item.id)" />
            </template>
            <template v-else>
              <span :id="data.item.id"></span>
              <input type="checkbox" :id="`checkbox${data.item.id}`" @change="onCheck(data.item.id)" />
            </template>
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
      fields: [
        { key: 'selected', label: '<p>test</p>', sortable: false, sortDirection: 'desc'},
        { key: 'id', label: 'ID', sortable: true, sortDirection: 'desc'},
        { key: 'name', label: 'Name', sortable: false},
        { key: 'language', label: 'LANGUAGE ', sortable: false},
        { key: 'email', label: 'EMAIL', sortable: false},
        { key: 'attr1', label: 'ATTRIBUTE 1', sortable: false},
        { key: 'attr2', label: 'ATTRIBUTE 2', sortable: false},
        { key: 'status', label: 'STATUS', sortable: false},
        { key: '', label: '', sortable: false}
      ],
      members: []
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
          status: 'survey Started',
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
      ]
  },
  components: {
    HelloWorld
  },
  methods: {
    onRowSelected(items) {
      this.selected = items
    },
    handleClick(data) {
      // document.getElementById(`checkbox${data.id}`).click();
    },
    onCheck(id) {
      document.getElementById(id).click();
    },
    changeFilterOn(val) {
      this.filterOn = val;
    }
  }
}
</script>

<style lang="scss">
.home {
  padding: 20px 10px;
  .table-border {
    border-radius: 10px;
    .justify-members {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      padding-left: 30px;
    }
  }
  .has-search {
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
  .selected {
    border: 1px solid #3366FF;
    margin-bottom: -1px;
    background: #EFF3FF;
  }
}
</style>