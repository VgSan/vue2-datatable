<template>
  <div>
    <code>query: {{ query }}</code>
    <datatable v-bind="$data" />
  </div>
</template>
<script>
import mockData from '../_mockData'

export default {
  data: () => ({
    supportBackup: true,
    columns: [
      { title: 'User ID', field: 'uid', sortable: true },
      { title: 'Username', field: 'name' },
      { title: 'Age', field: 'age', sortable: true },
      { title: 'Email', field: 'email' },
      { title: 'Country', field: 'country' }
    ],
    data: [],
    total: 0,
    query: {}
  }),
  watch: {
    query: {
      handler (query) {
        mockData(query).then(({ rows, total }) => {
          this.data = rows
          this.total = total
        })
      },
      deep: true
    }
  },
  methods: {
    SET_SUPPORT_BACKUP (k, v) {
      console.log('SET_SUPPORT_BACKUP')
      localStorage.setItem(k, JSON.stringify(v))
    },
    GET_SUPPORT_BACKUP (k) {
      console.log('GET_SUPPORT_BACKUP')
      try {
        return JSON.parse(localStorage.getItem(k))
      } catch (e) {
        localStorage.removeItem(k)
      }
    }
  }
}
</script>
