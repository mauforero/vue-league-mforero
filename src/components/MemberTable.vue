<template>
  <div v-if="!!team"> 
    <table v-if="team.members.length">
      <thead>
        <tr>
          <th>Name</th>
          <th>Timezone</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(member, index) in team.members" :key="index">
          <td>{{ member.name }}</td>
          <td>{{ member.timezone }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>Team has no members.</p>
  </div>
</template>

<script>
export default {
  name: 'MemberTable',
  props: {
    team: {
      type: Object,
      default: null
    }
  }
}
</script>