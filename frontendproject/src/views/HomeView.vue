<template>
  <div class="performance-review-form">
    <h1>Employee Performance Review</h1>
    <form @submit.prevent="submitForm">
      <!-- Employee Selection -->
      <div class="form-group">
        <label for="employee-select">Select Employee</label>
        <select id="employee-select" v-model="selectedEmployeeId" @change="populateEmployeeDetails" required>
          <option disabled value="">Select an employee</option>
          <option v-for="employee in employeeList" :key="employee.employeeId" :value="employee.employeeId">
            {{ employee.employeeId }} - {{ employee.name }}
          </option>
        </select>
      </div>
      <!-- Performance Metrics -->
      <div class="form-group">
        <label for="work-quality">Work Quality</label>
        <select id="work-quality" v-model="form.work_quality" required>
          <option disabled value="">Select a rating</option>
          <option value="1">1 - Poor</option>
          <option value="2">2 - Fair</option>
          <option value="3">3 - Good</option>
          <option value="4">4 - Very Good</option>
          <option value="5">5 - Excellent</option>
        </select>
      </div>
      <div class="form-group">
        <label for="attendance">Attendance</label>
        <select id="attendance" v-model="form.attendance" required>
          <option disabled value="">Select a rating</option>
          <option value="1">1 - Poor</option>
          <option value="2">2 - Fair</option>
          <option value="3">3 - Good</option>
          <option value="4">4 - Very Good</option>
          <option value="5">5 - Excellent</option>
        </select>
      </div>
      <div class="form-group">
        <label for="comments">Comments</label>
        <textarea
          id="comments"
          v-model="form.comments"
          placeholder="Enter additional comments"
        ></textarea>
      </div>
      <!-- Submit Button -->
      <div class="form-group">
        <button type="submit" @click="postReview()" class="submit-button" >Submit Review</button>
      </div>
    </form>
    <!-- Table to display form data after submission -->
    <table v-for="review in $store.state.reviews" :key="review.employee_id" class="review-table">
      <thead>
        <tr>
          <th>Employee ID</th>
          <th>Work Quality</th>
          <th>Attendance</th>
          <th>Comments</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ review.employee_id }}</td>
          <td>{{ review.work_quality }}</td>
          <td>{{ review.attendance }}</td>
          <td>{{ review.coments }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      employeeList: [
        { "employeeId": 1, "name": "Sibongile Nkosi", "position": "Software Engineer" },
        { "employeeId": 2, "name": "Lungile Moyo", "position": "HR Manager" },
        { "employeeId": 3, "name": "Thabo Molefe", "position": "Quality Analyst" },
        { "employeeId": 4, "name": "Keshav Naidoo", "position": "Sales Representative" },
        { "employeeId": 5, "name": "Zanele Khumalo", "position": "Marketing Specialist" },
        { "employeeId": 6, "name": "Business Analyst", "position": "Business Analyst" },
        { "employeeId": 7, "name": "Customer Support", "position": "Customer Support" },
        { "employeeId": 8, "name": "Product Manager", "position": "Product Manager" },
        { "employeeId": 9, "name": "Data Scientist", "position": "Data Scientist" },
        { "employeeId": 10, "name": "Operations Manager", "position": "Operations Manager" }
      ],
      form: {
        employee_id: '',
        position: '',
        work_quality: '',
        attendance: '',
        comments: ''
      },
      selectedEmployeeId: '',
      formSubmitted: false
    };
  },
  // mounted(){
  //   this.$store.dispatch('getReview');
  // },

  methods: {
    postReview() {
      this.$store.dispatch('postReview', this.review);
    },
    populateEmployeeDetails() {
      const selectedEmployee = this.employeeList.find(emp => emp.employeeId === this.selectedEmployeeId);
      if (selectedEmployee) {
        this.form.employee_id = selectedEmployee.employeeId;
        this.form.employee_name = selectedEmployee.name;
        this.form.position = selectedEmployee.position;
      }
    },
    submitForm() {
      this.formSubmitted = true;
    }
  }
};
</script>

<style scoped>
.performance-review-form {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #F9F9F9;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
.form-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}
input, select, textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.submit-button {
  width: 100%;
  padding: 10px;
  background-color: #28A745;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}
.submit-button:hover {
  background-color: #218838;
}
.review-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
.review-table th,
.review-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}
.review-table th {
  background-color: #F2F2F2;
  font-weight: bold;
}
</style>
