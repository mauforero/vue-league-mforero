<template>
  <div v-if="!!team" class="mt-4 py-4 border-y border-gray-300"> 
    <table v-if="team.members.length" class="w-full text-center">
      <thead>
        <tr>
          <th>Name</th>
          <th>Timezone</th>
          <th>Local Time</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(member, index) in membersWithTime" :key="index">
          <td class="text-left">{{ member.name }}</td>
          <td>{{ member.timezone }}</td>
          <td>{{ member.localTime }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>{{ team.name }} has no members.</p>
  </div>
</template>

<script>
import addSeconds from 'date-fns/addSeconds'
import { formatInTimeZone } from 'date-fns-tz'

export default {
  name: 'MemberTable',
  data()  {
    return {
      currentTime: new Date()
    }
  },
  props: {
    team: {
      type: Object,
      default: null
    }
  },
  computed: {
    membersWithTime: function() {
      return this.team.members.map((member) => {
        return {
          name: member.name,
          timezone: member.timezone,
          localTime: formatInTimeZone(this.currentTime, member.timezone, 'HH:mm:ss')
        }
      })
    }
  },
  mounted() {
    setInterval(() => {
      this.currentTime = addSeconds(this.currentTime, 1);
    }, 1000);
  }
}
</script>