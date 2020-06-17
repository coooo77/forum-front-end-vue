<template>
  <div class="container py-5">
    <!-- 1. 使用先前寫好的 AdminNav -->
    <AdminNav />

    <form class="my-4">
      <div class="form-row">
        <div class="col-auto">
          <input type="text" class="form-control" placeholder="新增餐廳類別..." v-model="newCategoryName" />
        </div>
        <div class="col-auto">
          <button type="button" class="btn btn-primary" @click.stop.prevent="createCategory">新增</button>
        </div>
      </div>
    </form>
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col" width="60">#</th>
          <th scope="col">Category Name</th>
          <th scope="col" width="210">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="category in categories" :key="category.id">
          <th scope="row">{{ category.id }}</th>
          <td class="position-relative"></td>
          <td class="position-relative">
            <div v-show="!category.isEditing" class="category-name">{{ category.name }}</div>
            <input
              v-show="category.isEditing"
              v-model="category.name"
              type="text"
              class="form-control"
            />
            <span v-show="category.isEditing" class="cancel" @click="handleCancel(category.id)">✕</span>
          </td>
          <td class="d-flex justify-content-between">
            <button
              v-show="!category.isEditing"
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="toggleIsEditing(category.id)"
            >Edit</button>
            <button
              v-show="category.isEditing"
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="updateCategory({ categoryId: category.id })"
            >Save</button>
            <button
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="deleteCategory(category.id)"
            >Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from "@/components/AdminNav";
// import uuid from "uuid/dist/v4";
import AdminAPI from "../apis/admin";
import { Toast } from "../utils/helpers";

export default {
  components: {
    AdminNav
  },
  // 3. 定義 Vue 中使用的 data 資料
  data() {
    return {
      categories: [],
      newCategoryName: ""
    };
  },
  // 5. 調用 `fetchCategories` 方法
  created() {
    this.fetchCategories();
  },
  methods: {
    // 4. 定義 `fetchCategories` 方法，把 `dummyData` 帶入 Vue 物件
    async fetchCategories() {
      try {
        // 在每一個 categories 中都添加一個 isEditing 屬性
        const { data, status, statusText } = await AdminAPI.categories.get();
        if (status !== 200) {
          throw new Error(statusText);
        }
        this.categories = data.categories.map(category => ({
          ...category,
          isEditing: false,
          nameCached: ""
        }));
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "warning",
          title: "找不到餐廳資料，請稍後嘗試"
        });
      }
    },
    async createCategory() {
      try {
        // TODO: 透過API告訴伺服器想要新增的餐廳類別...
        const { data } = await AdminAPI.categories.create({
          name: this.newCategoryName
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        // 清空原本欄位中的內容
        this.newCategoryName = "";
        await this.fetchCategories();
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "暫時不能增加類別，請稍後嘗試"
        });
      }
    },
    async deleteCategory(categoryId) {
      try {
        // TODO: 透過 API 告知伺服器欲刪除的餐廳類別
        const { status, statusText } = await AdminAPI.categories.deleteCategory(
          categoryId,
          this.newCategoryName
        );

        if (status !== 200) {
          throw new Error(statusText);
        }

        // 將該餐廳類別從陣列中移除
        this.categories = this.categories.filter(
          category => category.id !== categoryId
        );
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "無法刪除類別，請稍後嘗試"
        });
      }
    },
    toggleIsEditing(categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id === categoryId) {
          return {
            ...category,
            isEditing: !category.isEditing,
            nameCached: category.name
          };
        }

        return category;
      });
    },
    async updateCategory({ categoryId }) {
      try {
        // TODO: 透過 API 去向伺服器更新餐廳類別名稱
        const { status, statusText } = await AdminAPI.categories.updateCategory(
          categoryId,
          this.newCategoryName
        );

        if (status !== 200) {
          throw new Error(statusText);
        }

        this.toggleIsEditing(categoryId);
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "無法修改類別，請稍後嘗試"
        });
      }
    },
    handleCancel(categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id === categoryId) {
          return {
            ...category,

            // 把原本的餐廳類別名稱還回去
            name: category.nameCached
          };
        }

        return category;
      });

      this.toggleIsEditing(categoryId);
    }
  }
};
</script>

<style scoped>
.category-name {
  padding: 0.375rem 0.75rem;
  border: 1px solid transparent;
  outline: 0;
  cursor: auto;
}

.btn-link {
  width: 62px;
}

.cancel {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 25px;
  height: 25px;
  border: 1px solid #aaaaaa;
  border-radius: 50%;
  user-select: none;
  cursor: pointer;
  font-size: 12px;
}
</style>