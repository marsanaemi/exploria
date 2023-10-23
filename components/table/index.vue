<template>
  <div>
    <table>
      <thead>
      <tr>
        <th v-for="(header, index) in tableHeaders" :key="index">{{ header }}</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index) in paginatedData" :key="index">
        <td v-for="(value, key) in item" :key="key">{{ value }}</td>
      </tr>
      </tbody>
    </table>

    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Table',
  props: {
    data: Array, // The data to be displayed in the table
    itemsPerPage: Number, // Number of items per page
    tableHeaders: Array, // An array of table headers
  },
  data() {
    return {
      currentPage: 1,
    };
  },
  computed: {
    paginatedData() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.data.slice(startIndex, endIndex);
    },
    totalPages() {
      return Math.ceil(this.data.length / this.itemsPerPage);
    },
  },
  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
  },
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
</style>