<template>
  <div class="avengers-container">
    <!-- Avengers-themed title -->
    <h2 class="avengers-title">Avengers Roster</h2>
    
    <!-- Avengers-themed table -->
    <table class="avengers-table">
      <!-- Table headers -->
      <thead>
        <tr>
          <th>Hero</th>
          <th>Alias</th>
          <th>Power Level</th>
          <th>Amount</th>
          <th>Actions</th> <!-- New actions column -->
        </tr>
      </thead>
      <!-- Table body -->
      <tbody>
        <tr v-for="(row, index) in paginatedData" :key="index">
          <td>{{ row.hero }}</td>
          <td>{{ row.alias }}</td>
          <td>{{ row.powerLevel }}</td>
          <td>{{ row.amount }}</td>
          <td>
            <!-- Action buttons -->
            <button class="action-button like-button" @click="handleLike(row.hero)">👍 Like</button>
            <button class="action-button edit-button" @click="handleEdit(row.hero)">✏️ Edit</button>
            <button class="action-button delete-button" @click="handleDelete(row.hero)">❌ Delete</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Pagination controls -->
    <div class="pagination">
      <button @click="prevPage" :disabled="currentPage === 1" class="pagination-button">Previous</button>
      <button @click="nextPage" :disabled="currentPage === totalPages" class="pagination-button">Next</button>
      <span class="pagination-info">Page {{ currentPage }} of {{ totalPages }}</span>
    </div>

    <!-- Notification -->
    <div v-if="notification" class="notification">
      {{ notification }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: [
        { hero: "Tony Stark", alias: "Iron Man", powerLevel: "95", amount: "$1,000,000" },
        { hero: "Steve Rogers", alias: "Captain America", powerLevel: "90", amount: "$500,000" },
        { hero: "Thor Odinson", alias: "Thor", powerLevel: "100", amount: "Priceless" },
        { hero: "Bruce Banner", alias: "Hulk", powerLevel: "98", amount: "$200,000" },
        { hero: "Natasha Romanoff", alias: "Black Widow", powerLevel: "85", amount: "$150,000" },
      ],
      currentPage: 1,
      rowsPerPage: 3, // Display only 3 rows per page
      notification: '', // Notification message
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.rows.length / this.rowsPerPage);
    },
    paginatedData() {
      const start = (this.currentPage - 1) * this.rowsPerPage;
      const end = start + this.rowsPerPage;
      return this.rows.slice(start, end);
    },
  },
  methods: {
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    handleLike(hero) {
      this.notification = `You liked ${hero}!`;
      this.clearNotification();
    },
    handleEdit(hero) {
      this.notification = `You edited ${hero}!`;
      this.clearNotification();
    },
    handleDelete(hero) {
      this.notification = `You deleted ${hero}!`;
      this.clearNotification();
    },
    clearNotification() {
      setTimeout(() => {
        this.notification = '';
      }, 2000); // Clear the notification after 2 seconds
    },
  },
};
</script>

<style scoped>
/* Font and color customization */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.avengers-container {
  font-family: 'Roboto', sans-serif;
  background-color: #f7f9fc;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
}

.avengers-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 700;
  color: #34495e;
  margin-bottom: 20px;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.avengers-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 10px;
  margin-bottom: 20px;
}

th, td {
  padding: 12px 16px;
  border-bottom: 2px solid #ecf0f1;
  text-align: left;
  background-color: #ffffff;
  border-radius: 8px;
  font-weight: 500;
}

th {
  background-color: #2c3e50;
  color: #ffffff;
  text-transform: uppercase;
}

td {
  color: #2c3e50;
}

.action-button {
  padding: 8px 12px;
  margin-right: 5px;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  color: #ffffff;
  transition: background-color 0.3s;
}

.like-button {
  background-color: #27ae60;
}

.like-button:hover {
  background-color: #2ecc71;
}

.edit-button {
  background-color: #f39c12;
}

.edit-button:hover {
  background-color: #e67e22;
}

.delete-button {
  background-color: #c0392b;
}

.delete-button:hover {
  background-color: #e74c3c;
}

.pagination {
  text-align: center;
  margin-top: 20px;
}

.pagination-button {
  padding: 8px 16px;
  margin: 0 5px;
  border: none;
  background-color: #2980b9;
  color: #ffffff;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s;
}

.pagination-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}

.pagination-button:hover:not(:disabled) {
  background-color: #3498db;
}

.pagination-info {
  font-size: 1rem;
  font-weight: bold;
  color: #34495e;
}

.notification {
  margin-top: 20px;
  padding: 15px;
  background-color: #4caf50;
  color: white;
  border-radius: 5px;
  text-align: center;
  font-weight: bold;
}
</style>
