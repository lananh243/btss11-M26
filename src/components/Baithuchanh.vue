<template>
  <div class="container">
    <div class="header">
      <b>Quản lý mượn trả sách</b>
      <div class="information">
        <select v-model="filterStatus" @change="filterBorrowings">
          <option value="">Lọc theo trạng thái</option>
          <option value="Đã trả">Đã trả</option>
          <option value="Chưa trả">Chưa trả</option>
        </select>
        <button @click="showAddForm = true">Thêm thông tin</button>
      </div>
    </div>

    <div>
      <table>
        <thead>
          <tr>
            <th>STT</th>
            <th>Tên sách</th>
            <th>Sinh viên mượn</th>
            <th>Ngày mượn</th>
            <th>Ngày trả</th>
            <th>Trạng thái</th>
            <th>Chức năng</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(borrowing, index) in filteredBorrowings"
            :key="borrowing.id"
          >
            <td>{{ index + 1 }}</td>
            <td>{{ borrowing.bookName }}</td>
            <td>{{ borrowing.borrowerName }}</td>
            <td>{{ borrowing.borrowDate }}</td>
            <td>{{ borrowing.returnDate }}</td>
            <td>
              <select
                v-model="borrowing.status"
                @change="updateStatus(borrowing.id, borrowing.status)"
              >
                <option value="Chưa trả">Chưa trả</option>
                <option value="Đã trả">Đã trả</option>
              </select>
            </td>
            <td>
              <div class="btn">
                <button @click="editBorrowing(borrowing)">Sửa</button>
                <button @click="deleteBorrowing(borrowing.id)">Xóa</button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Form thêm thông tin -->
    <div v-if="showAddForm" class="modal">
      <div class="modal-content">
        <h3>Thêm thông tin mượn sách</h3>
        <input
          type="text"
          v-model="newBorrowing.bookName"
          placeholder="Tên sách"
        />
        <input
          type="text"
          v-model="newBorrowing.borrowerName"
          placeholder="Tên sinh viên mượn"
        />
        <input type="date" v-model="newBorrowing.borrowDate" />
        <input type="date" v-model="newBorrowing.returnDate" />
        <select v-model="newBorrowing.status">
          <option value="Chưa trả">Chưa trả</option>
          <option value="Đã trả">Đã trả</option>
        </select>
        <div class="modal-buttons">
          <button @click="addBorrowing">Thêm</button>
          <button @click="showAddForm = false">Đóng</button>
        </div>
      </div>
    </div>

    <!-- Form sửa thông tin (nếu cần) -->
    <div v-if="showEditForm" class="modal">
      <div class="modal-content">
        <h3>Sửa thông tin mượn sách</h3>
        <input
          type="text"
          v-model="editBorrowingData.bookName"
          placeholder="Tên sách"
        />
        <input
          type="text"
          v-model="editBorrowingData.borrowerName"
          placeholder="Tên sinh viên mượn"
        />
        <input type="date" v-model="editBorrowingData.borrowDate" />
        <input type="date" v-model="editBorrowingData.returnDate" />
        <select v-model="editBorrowingData.status">
          <option value="Chưa trả">Chưa trả</option>
          <option value="Đã trả">Đã trả</option>
        </select>
        <div class="modal-buttons">
          <button @click="saveEditedBorrowing">Lưu</button>
          <button @click="showEditForm = false">Đóng</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const borrowings = ref([]);

const filterStatus = ref("");
const showAddForm = ref(false);
const showEditForm = ref(false);
const newBorrowing = ref({
  id: null,
  bookName: "",
  borrowerName: "",
  borrowDate: "",
  returnDate: "",
  status: "Chưa trả",
});

const editBorrowingData = ref(null);

const filteredBorrowings = computed(() => {
  if (!filterStatus.value) {
    return borrowings.value;
  }
  return borrowings.value.filter(
    (borrowing) => borrowing.status === filterStatus.value
  );
});

const addBorrowing = () => {
  newBorrowing.value.id = Date.now();
  borrowings.value.push({ ...newBorrowing.value });
  showAddForm.value = false;
  resetNewBorrowing();
};

const editBorrowing = (borrowing) => {
  editBorrowingData.value = { ...borrowing };
  showEditForm.value = true;
};

const saveEditedBorrowing = () => {
  const index = borrowings.value.findIndex(
    (b) => b.id === editBorrowingData.value.id
  );
  if (index !== -1) {
    borrowings.value[index] = { ...editBorrowingData.value };
  }
  showEditForm.value = false;
};

const deleteBorrowing = (id) => {
  borrowings.value = borrowings.value.filter((b) => b.id !== id);
};

const updateStatus = (id, status) => {
  const borrowing = borrowings.value.find((b) => b.id === id);
  if (borrowing) {
    borrowing.status = status;
  }
};

const resetNewBorrowing = () => {
  newBorrowing.value = {
    id: null,
    bookName: "",
    borrowerName: "",
    borrowDate: "",
    returnDate: "",
    status: "Chưa trả",
  };
};
</script>

<style scoped>
.container {
  width: 800px;
  padding: 50px;
  border: 1px solid grey;
}
.information {
  display: flex;
  gap: 20px;
}
.header {
  display: flex;
  justify-content: space-between;
}
table {
  font-family: Arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  margin-top: 30px;
}
td,
th {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;
}
.btn {
  display: flex;
  justify-content: center;
  gap: 18px;
}
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 20px;
  border: 1px solid black;
}
.modal-buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}
</style>
