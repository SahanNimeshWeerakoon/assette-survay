<template>
  <div class="home">
  <b-row class="align-center">
    <b-col cols="2" class="text-center"><b>2 Members Selected</b></b-col>
    <b-col cols="6" class="text-center"></b-col>
    <b-col cols="4" class="text-center">
      <b-col cols="5" class="text-center">
        <b-dropdown id="dropdown-right" :text=" filterOn !== '' ? filterOn : 'Filter By All'" variant="outline-primary" v-model="filterOn" class="m-md-2">
          <b-dropdown-item>All</b-dropdown-item>
          <b-dropdown-item>1 reminder sent</b-dropdown-item>
          <b-dropdown-item>Started</b-dropdown-item>
          <b-dropdown-item>Completed</b-dropdown-item>
          <b-dropdown-item>2 reminders sent</b-dropdown-item>
        </b-dropdown>
      </b-col>
      <b-col cols="7" class="text-center mt-md-2 mb-md-2">
        <div class="form-group has-search">
          <span class="fa fa-search form-control-feedback"></span>
          <input type="text" v-model="filter" class="form-control" placeholder="Search">
        </div>
      </b-col>
    </b-col>
    test{{ filterOn }}
  </b-row>
    <b-table
        :items="members"
        :filter="filter"
        :filter-included-fields="[filterOn]"
        responsive="sm"
      ></b-table>
    <!--<b-container-fluid class="bv-example-row rounded">
      <b-row class="border">
        <b-col cols="2" class="text-center"><b>2 Members Selected</b></b-col>
        <b-col cols="6" class="text-center"></b-col>
        <b-col cols="4" class="text-center">
          <b-row class="align-center">
            <b-col cols="5" class="text-center">
              <b-dropdown id="dropdown-right" text="Filtered By All" variant="outline-primary" class="m-md-2">
                <b-dropdown-item>All</b-dropdown-item>
                <b-dropdown-item>1 reminder sent</b-dropdown-item>
                <b-dropdown-item>Started</b-dropdown-item>
                <b-dropdown-item>Completed</b-dropdown-item>
                <b-dropdown-item>2 reminders sent</b-dropdown-item>
              </b-dropdown>
            </b-col>
            <b-col cols="7" class="text-center mt-md-2 mb-md-2">
              <div class="form-group has-search">
                <span class="fa fa-search form-control-feedback"></span>
                <input type="text" class="form-control" placeholder="Search">
              </div>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
      <b-row class="border">
        <b-col class="text-center" cols="1"><input type="checkbox" id="all" /></b-col>
        <b-col class="text-left" cols="1">ID <img alt="id icon" src="../assets/idIcon.png" /></b-col>
        <b-col class="text-left" cols="1">NAME</b-col>
        <b-col class="text-left" cols="1">LANGUAGE</b-col>
        <b-col class="text-left" cols="4">EMAIL</b-col>
        <b-col class="text-left" cols="1">ATTRIBUTE 1</b-col>
        <b-col class="text-left" cols="1">ATTRIBUTE 2</b-col>
        <b-col class="text-left" cols="1">STATUS</b-col>
        <b-col class="text-right" cols="1"></b-col>
      </b-row>
      <b-row :class="member.selected ? 'selected' : ''" v-for="member in members">
        <b-col class="text-center" cols="1"><input type="checkbox" :checked="member.selected ? true : false " /></b-col>
        <b-col class="text-left" cols="1">{{ member.id }}</b-col>
        <b-col class="text-left" cols="1">{{ member.name }}</b-col>
        <b-col class="text-left" cols="1">{{ member.language }}</b-col>
        <b-col class="text-left" cols="4">{{ member.email }}</b-col>
        <b-col class="text-left" cols="1">{{ member.attr1 }}</b-col>
        <b-col class="text-left" cols="1">{{ member.attr2 }}</b-col>
        <b-col class="text-left" cols="1">{{ member.status }}</b-col>
        <b-col class="text-right" cols="1"></b-col>
      </b-row>
    </b-container-fluid>-->
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
      filterOn: "test",
      fields: ["ID", "NANME", "LANGUAGE", "EMAIL", "ATTRIBUTE 1", "ATTRIBUTE 2", "STATUS", ""],
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
    changeFilterOn() {
      console.log("test");
    }
  }
}
</script>

<style lang="scss">
.home {
  padding: 20px 10px;
  /*.has-search .form-control {
      padding-left: 2.375rem;
  }

  .has-search .form-control-feedback {
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
  .selected {
    border: 1px solid #3366FF;
    margin-bottom: -1px;
    background: #EFF3FF;
  }*/
}
</style>