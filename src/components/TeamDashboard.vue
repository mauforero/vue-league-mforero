<template>
    <div class="container mx-auto mt-4 px-4 sm:px-0">
      <div>
        <div class="grid grid-flow-row sm:grid-flow-col gap-4 max-w-md">
          <select name="teams" id="teams" v-model="currentTeam">
            <option :value="null">Select a team</option>
            <option v-for="(team, index) in teams" :key="index" :value="team">
              {{ team.name }}
            </option>
          </select>
          <input 
            type="text" 
            name="newTeam" 
            id="newTeam" 
            placeholder="New Team"
            v-model="newTeam" />
          <input 
            type="button" 
            value="Add Team" 
            @click="addTeam" 
            :disabled="newTeam.length === 0" 
            :class="['btn', { 'btn-disabled': newTeam.length === 0 }]" />
        </div>

      </div>
      <div>
        <MemberTable :team="currentTeam" />
        <div v-if="!!currentTeam" class="mt-4 py-4">
          <div class="grid grid-flow-row sm:grid-flow-col gap-4 max-w-md">
            <input type="text" name="newMember" id="newMember" v-model="newMember" placeholder="Member Name">
            <select name="teams" id="teams" v-model="selectedTimezone" class="max-w-xs">
              <option value="">Select a timezone</option>
              <option v-for="(timezone, index) in timezones" :key="index" :value="timezone">
                {{ timezone }}
              </option>
            </select>
            <input type="button" value="Add Member" @click="addMember">
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import MemberTable from './MemberTable.vue';

export default {
  name: 'TeamDashboard',
  data() {
    return {
      teams: [
        {
          name: 'SIR',
          members: [
            {
              name: 'Jose Ospina',
              timezone: 'America/Bogota'
            },
            {
              name: 'Mauricio Forero',
              timezone: 'America/Bogota'
            },
            {
              name: 'David Longan',
              timezone: 'Europe/London'
            },
          ]
        },
        {
          name: 'Huge Inc',
          members: [
            {
              name: 'Jose Ospina',
              timezone: 'America/Bogota'
            },
            {
              name: 'Mauricio Forero',
              timezone: 'America/Bogota'
            },
            {
              name: 'Carolina Napoli',
              timezone: 'America/New_York'
            },
          ]
        },
      ],
      currentTeam: null,
      timezones:[],
      newTeam: "",
      newMember: "",
      selectedTimezone: ""
    }
  },
  components: {
    MemberTable
  },
  methods: {
    addTeam: function() {
      if (this.newTeam.length) {
        this.teams.push({
          name: this.newTeam,
          members: []
        });
        this.newTeam = "";
      }
    },
    addMember: function() {
      if (this.newMember.length && this.selectedTimezone.length) {
        this.currentTeam.members.push({
          name: this.newMember,
          timezone: this.selectedTimezone
        });
        this.newMember = "";
        this.selectedTimezone = "";
      }
    }
  },
  mounted() {
    for (const timeZone of Intl.supportedValuesOf('timeZone')) {
      this.timezones.push(timeZone);
    }
  }
}
</script>