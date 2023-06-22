<template>
  <table>
    <thead>
      <tr>
        <th>Tên</th>
        <th @click="sortBy('test')">Ngày & Giờ</th>
        <!-- Thêm các cột khác nếu cần -->
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in sortedItems" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.datetime }}</td>
        <!-- Hiển thị các thuộc tính khác của mục nếu cần -->
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { id: 1, name: "John", datetime: "2023/06/15" },
        { id: 2, name: "Alice", datetime: "2023/06/14" },
        { id: 3, name: "Tom", datetime: "2023/06/11" },
        { id: 4, name: "ToNy", datetime: "2023/06/18" },
        // Thêm các mục khác nếu cần
      ],
      sortKey: "", // Khóa để lưu thuộc tính dùng để sắp xếp
      sortDirection: "asc", // Hướng sắp xếp mặc định là từ trước đến sau
    };
  },
  computed: {
    sortedItems() {
      return this.items.sort((a, b) => {
        const valueA = a[this.sortKey];
        const valueB = b[this.sortKey];

        if (this.sortDirection === "asc") {
          return valueA < valueB ? -1 : valueA > valueB ? 1 : 0;
        } else {
          return valueA > valueB ? -1 : valueA < valueB ? 1 : 0;
        }
      });
    },
  },
  methods: {
    sortBy(key) {
      if (this.sortKey === key) {
        this.sortDirection = this.sortDirection === "asc" ? "desc" : "asc";
      } else {
        this.sortKey = key;
        this.sortDirection = "asc";
      }
    },
  },
};
</script>
