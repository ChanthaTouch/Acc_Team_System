<template>
  <div class="p-4">
    <!-- Search and Action Button -->
    <div class="flex justify-between items-center mb-4">
      <input
        type="text"
        placeholder="Search PR Code, Item Code, Description..."
        class="w-full max-w-md px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring focus:border-blue-300"
      />
      <button
        class="ml-4 bg-gray-900 text-white py-2 px-4 rounded-lg hover:bg-gray-700"
      >
        PR Pending
      </button>
    </div>

    <!-- Tabs for Form, Listing, Dashboard, Report, Filtering -->
    <div class="mb-4">
      <div class="flex border-b-2">
        <button
          class="py-2 px-4 text-gray-600 hover:text-blue-600 border-b-2 border-transparent hover:border-blue-600"
          @click="activeTab = 'form'"
        >
          Form
        </button>
        <button
          class="py-2 px-4 text-gray-600 hover:text-blue-600 border-b-2 border-transparent hover:border-blue-600"
          @click="activeTab = 'listing'"
        >
          Listing
        </button>
        <button
          class="py-2 px-4 text-gray-600 hover:text-blue-600 border-b-2 border-transparent hover:border-blue-600"
          @click="activeTab = 'dashboard'"
        >
          Dashboard
        </button>
        <button
          class="py-2 px-4 text-gray-600 hover:text-blue-600 border-b-2 border-transparent hover:border-blue-600"
          @click="activeTab = 'report'"
        >
          Report
        </button>
      </div>
    </div>

    <!-- Conditional Tab Content -->
    <div v-if="activeTab === 'form'">
      <!-- Add New Form Section -->
      <div class="mb-4">
        <button
          @click="openModal('add')"
          class="bg-green-500 text-white py-2 px-4 rounded-lg hover:bg-green-400"
        >
          Add New
        </button>
        <button
          @click="openModal('edit')"
          class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-400 ml-2"
        >
          Edit
        </button>
        <button
          @click="openModal('detail')"
          class="bg-yellow-500 text-white py-2 px-4 rounded-lg hover:bg-yellow-400 ml-2"
        >
          Detail View
        </button>

      </div>
    </div>

    <!-- Listing Tab -->
    <div v-if="activeTab === 'listing'">
      <div class="overflow-x-auto">
        <table class="w-full border-collapse border border-gray-200 shadow-sm">
          <thead class="bg-gray-100">
            <tr>
              <th class="border px-4 py-2 text-left">#</th>
              <th class="border px-4 py-2 text-left">PR-ID</th>
              <th class="border px-4 py-2 text-left">Request Date</th>
              <th class="border px-4 py-2 text-left">Due Date</th>
              <th class="border px-4 py-2 text-left">Drawing No</th>
              <th class="border px-4 py-2 text-left">Purpose</th>
              <th class="border px-4 py-2 text-left">Requested By</th>
              <th class="border px-4 py-2 text-left">Checked By</th>
              <th class="border px-4 py-2 text-left">Verified By</th>
              <th class="border px-4 py-2 text-left">Approved By</th>
              <th class="border px-4 py-2 text-left">Approved Date</th>
              <th class="border px-4 py-2 text-left">Status</th>
              <th class="border px-4 py-2 text-left">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr class="hover:bg-gray-50" v-for="(row, index) in rows" :key="row.id">
              <td class="border px-4 py-2">{{ index + 1 }}</td>
              <td class="border px-4 py-2">{{ row.pr_id }}</td>
              <td class="border px-4 py-2">{{ row.request_date }}</td>
              <td class="border px-4 py-2">{{ row.due_date }}</td>
              <td class="border px-4 py-2">{{ row.drawing_no }}</td>
              <td class="border px-4 py-2">{{ row.purpose }}</td>
              <td class="border px-4 py-2">{{ row.requested_by }}</td>
              <td class="border px-4 py-2">{{ row.checked_by }}</td>
              <td class="border px-4 py-2">{{ row.verified_by }}</td>
              <td class="border px-4 py-2">{{ row.approved_by }}</td>
              <td class="border px-4 py-2">{{ row.approved_date }}</td>
              <td class="border px-4 py-2">
                <span :class="getStatusClass(row.status)">
                  {{ row.status }}
                </span>
              </td>
              <td class="border px-4 py-2 flex space-x-2">
                <button @click="openModal('edit', row)" title="Edit">
                  <i class="fas fa-edit text-blue-500"></i>
                </button>
                <button @click="openModal('delete', row)" title="Delete">
                  <i class="fas fa-trash-alt text-red-500"></i>
                </button>
                <button @click="openModal('detail', row)" title="Details">
                  <i class="fas fa-file-alt text-gray-500"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <!-- ------------Form Detail view ----- -->
     <div v-if="activeModal === 'detail' ">
      <div class=" w-full h-full bg-white">
        
      </div>
     </div>

    <!-- Modal Form Edit and Add New -->
    <div
      v-if="activeModal === 'add' || activeModal === 'edit'"
      class="fixed inset-0 z-50 flex items-center justify-center bg-gray-900 bg-opacity-50"
    >
      <div class="bg-white p-8 rounded-lg shadow-lg w-2/3">
        <h2 class="text-xl font-semibold mb-4">
          {{ activeModal === 'add' ? 'Add New Form' : 'Edit Form' }}
        </h2>
        <form @submit.prevent="activeModal === 'add' ? addNewData() : saveEdit()">
          <div class="grid grid-cols-2 gap-4">
            <div>
              <label for="pr_id" class="block text-gray-700">PR ID</label>
              <input
                type="text"
                v-model="currentForm.pr_id"
                id="pr_id"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="request_date" class="block text-gray-700">Request Date</label>
              <input
                type="date"
                v-model="currentForm.request_date"
                id="request_date"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="due_date" class="block text-gray-700">Due Date</label>
              <input
                type="date"
                v-model="currentForm.due_date"
                id="due_date"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="drawing_no" class="block text-gray-700">Drawing No</label>
              <input
                type="text"
                v-model="currentForm.drawing_no"
                id="drawing_no"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="purpose" class="block text-gray-700">Purpose</label>
              <input
                type="text"
                v-model="currentForm.purpose"
                id="purpose"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="requested_by" class="block text-gray-700">Requested By</label>
              <input
                type="text"
                v-model="currentForm.requested_by"
                id="requested_by"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="checked_by" class="block text-gray-700">Checked By</label>
              <input
                type="text"
                v-model="currentForm.checked_by"
                id="checked_by"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
            <div>
              <label for="verified_by" class="block text-gray-700">Verified By</label>
              <input
                type="text"
                v-model="currentForm.verified_by"
                id="verified_by"
                class="w-full px-4 py-2 border rounded-lg"
                required
              />
            </div>
          </div>
          <div class="mt-4 text-right">
            <button
              type="submit"
              class="bg-green-500 text-white py-2 px-6 rounded-lg hover:bg-green-400"
            >
              Save
            </button>
            <button
              type="button"
              @click="closeModal"
              class="ml-2 bg-gray-500 text-white py-2 px-6 rounded-lg hover:bg-gray-400"
            >
              Cancel
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTab: "form",
      activeModal: null,
      currentForm: {
        pr_id: "",
        request_date: "",
        due_date: "",
        drawing_no: "",
        purpose: "",
        requested_by: "",
        checked_by: "",
        verified_by: "",
      },
      rows: [
        {
          id: 1,
          pr_id: "CMT-PR2412-0003",
          request_date: "2024-12-06",
          due_date: "2024-12-14",
          drawing_no: "Kumatsu-01",
          purpose: "For Head work",
          requested_by: "YUN Tola",
          checked_by: "YUN Tola",
          verified_by: "KEAT Khoun",
          approved_by: "-",
          approved_date: "-",
          status: "Approve",
        },
        {
          id: 2,
          pr_id: "CMT-PR2412-0004",
          request_date: "2024-12-06",
          due_date: "2024-12-14",
          drawing_no: "Kumatsu-01",
          purpose: "For Head work",
          requested_by: "YUN Tola",
          checked_by: "YUN Tola",
          verified_by: "KEAT Khoun",
          approved_by: "-",
          approved_date: "-",
          status: "Pending",
        },
      ],
    };
  },
  methods: {
    openModal(modalType, row = null) {
      this.activeModal = modalType;
      if (modalType === "edit" && row) {
        this.currentForm = { ...row };
      } else if (modalType === "add") {
        this.currentForm = {
          pr_id: "",
          request_date: "",
          due_date: "",
          drawing_no: "",
          purpose: "",
          requested_by: "",
          checked_by: "",
          verified_by: "",
        };
      }
    },
    closeModal() {
      this.activeModal = null;
    },
    addNewData() {
      this.rows.push({ ...this.currentForm, id: this.rows.length + 1, status: "Pending" });
      this.closeModal();
    },
    saveEdit() {
      const index = this.rows.findIndex((row) => row.id === this.currentForm.id);
      if (index !== -1) {
        this.rows.splice(index, 1, { ...this.currentForm });
      }
      this.closeModal();
    },
    getStatusClass(status) {
      if (status === "Approve") {
        return "bg-green-200 text-green-800 px-3 py-1 rounded-full";
      } else if (status === "Pending") {
        return "bg-red-200 text-red-800 px-3 py-1 rounded-full";
      }
      return "bg-yellow-200 text-yellow-800 px-3 py-1 rounded-full";
    },
  },
};
</script>

<style scoped>
/* Add any custom styles here */
</style>
