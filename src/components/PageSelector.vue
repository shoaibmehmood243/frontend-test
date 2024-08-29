<template>
  <div class="page-selector">
    <div class="select-all">
      <label>
        <span>Select All</span>
        <input type="checkbox" v-model="selectAll" @change="toggleAll" />
        <span class="checkmark"></span>
      </label>
    </div>
    <div class="divider"></div>
    <div class="page-list">
      <div v-for="page in pages" :key="page.id" class="page-item">
        <label>
          <span>{{ page.name }}</span>
          <input
            type="checkbox"
            :id="page.id"
            v-model="page.selected"
            @change="updateSelectAll"
          />
          <span class="checkmark"></span>
        </label>
      </div>
    </div>
    <div class="divider"></div>
    <div>
      <button @click="showSelectedPages">Done</button>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed } from "vue";

export default {
  name: "PageSelector",
  setup() {
    const pages = reactive([
      { id: 1, name: "Page 1", selected: false },
      { id: 2, name: "Page 2", selected: false },
      { id: 3, name: "Page 3", selected: false },
      { id: 4, name: "Page 4", selected: false },
    ]);

    const selectAll = ref(false);

    const toggleAll = () => {
      pages.forEach((page) => (page.selected = selectAll.value));
    };

    const updateSelectAll = () => {
      selectAll.value = pages.every((page) => page.selected);
    };

    const selectedPages = computed(() => {
      return pages.filter((page) => page.selected);
    });

    const showSelectedPages = () => {
      const selected = selectedPages.value.map(page => page.name).join(", ");
      if (selected) {
        alert(`Selected pages: ${selected}`);
      } else {
        alert("No pages selected");
      }
    };

    return {
      pages,
      selectAll,
      toggleAll,
      updateSelectAll,
      selectedPages,
      showSelectedPages,
    };
  },
};
</script>

<style scoped>
.page-selector {
  max-width: 370px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #eeeeee;
  box-shadow: 0px 8px 15px 0px #1414141f;
  border-radius: 6px;
}

.select-all {
  margin-bottom: 10px;
}

.divider {
  margin: 20px 0;
  height: 0.7px;
  background: #cdcdcd;
}

.page-list {
  display: flex;
  flex-direction: column;
}

.page-item {
  margin-bottom: 15px;
}

label {
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  position: relative;
  padding-right: 30px;
}

span {
  font-size: 14px;
  font-weight: 400;
  line-height: 18.2px;
  text-align: left;
  color: #1f2128;
}

input[type="checkbox"] {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  height: 18px;
  width: 18px;
  background-color: #fff;
  border: 1px solid #BDBDBD;
  border-radius: 6px;
}

input[type="checkbox"]:checked ~ .checkmark {
  background-color: #2469F6;
  border-color: #2469F6;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

input[type="checkbox"]:checked ~ .checkmark:after {
  display: block;
}

.checkmark:after {
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 1px 1px 0;
  transform: rotate(45deg);
}

button {
  width: 100%;
  background: #ffce22;
  padding: 10px 20px;
  border-radius: 4px;
  border: none;
  outline: none;
  cursor: pointer;
  font-size: 14px;
  color: #1f2128;
}

button:hover {
  background: #ffd74a;
}
</style>
