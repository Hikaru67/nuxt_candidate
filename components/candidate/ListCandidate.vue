<template>
  <div>
    <!--    <CDataTable
      :items="dataCandidate"
      :fields="fields"
      :items-per-page="5"
      items-per-page-select
      pagination
    >
      &lt;!&ndash;      <template #position="{item}">
        <td>
          {{ getPosition(item.position) }}
        </td>
      </template>
      <template #created_at="{item}">
        <td>
          {{ convertDate(item.created_at) }}
        </td>
      </template>
      <template #status="{item}">
        <td>
          {{ getStatus(item.status) }}
        </td>
      </template>
      <template #origin="{item}">
        <td>
          {{ getOrigin(item.origin) }}
        </td>
      </template>&ndash;&gt;
      <template #delete="{item}">
        <td class="py-2">
          <CButton color="success">
            <nuxt-link :to="`/candidate/${item.id}`">
              <CIcon :content="$options.pencil" />
            </nuxt-link>
          </CButton>
          <CButton
            color="danger"
            @click="showModal(item.id)">
            <CIcon :content="$options.trash" />
          </CButton>
        </td>
      </template>
    </CDataTable>
    <CModal
      :show.sync="warningModal"
      title="Delete"
      color="warning"
    >
      Do you want to delete ?
      <div
        slot="footer"
        class="w-100">
        <CButton
          style="border-radius: .2rem; color: white;"
          color="danger"
          class="ml-1 mr-1 float-right"
          @click="warningModal = false"
        >
          No
        </CButton>
        <CButton
          style="border-radius: .2rem; color: white;"
          color="danger"
          class="ml-1 mr-1 float-right"
          @click="deleteData(id)"
        >
          Yes
        </CButton>
      </div>
    </CModal>-->
  </div>
</template>

<script>
import axios from 'axios'

const fields = [
  { key: 'firstName', label: 'First name' },
  { key: 'lastName', label: 'Last name' },
  { key: 'phone', label: 'Phone' },
  { key: 'email', label: 'Email' },
  { key: 'position', label: 'Position' },
  { key: 'origin', label: 'Origin' },
  { key: 'status', label: 'Status' },
  { key: 'created_at', label: 'Date received' },
  {
    key: 'delete',
    label: ''
  }
]

export default {
  name: 'ListCandidate',
  data: function() {
    return {
      fields: fields,
      dataCandidate: []
    }
  },
  mounted() {
    axios.get('http://localhost:8000/api/candidates').then(response => {
      this.dataCandidate = response.data
    })
  },

  methods: {
    deleteData(id) {
      axios
        .delete('http://localhost:8000/api/candidates/', id)
        .then(response => {
          this.dataCandidate = response.data
        })
    }
  }
}
</script>

<style scoped>
</style>
