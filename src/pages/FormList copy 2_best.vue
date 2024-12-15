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
        <div class="mb-4">
          <button @click="openModal('add')" class="bg-green-500 text-white py-2 px-4 rounded-lg hover:bg-green-400">Add New</button>
          <button @click="openModal('edit')" class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-400">Edit</button>
          <button @click="openModal('detail')" class="bg-yellow-500 text-white py-2 px-4 rounded-lg hover:bg-yellow-400">Detail View</button>
        </div>
      </div>
  
      <div v-if="activeTab === 'listing'">
        <!-- Responsive Table -->
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
                  <button @click="openModal('print', row)" title="Print">
                    <i class="fas fa-print text-gray-500"></i>
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
  
      <div v-if="activeTab === 'dashboard'">
        <!-- Dashboard content will go here -->
        <h2>Dashboard Design & Management</h2>
      </div>
  
      <div v-if="activeTab === 'report'">
        <!-- Report content will go here -->
        <h2>Report Design & Management</h2>
      </div>
  
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        activeTab: 'form', // Default tab
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
      getStatusClass(status) {
        if (status === 'Approve') {
          return 'bg-green-200 text-green-800 px-3 py-1 rounded-full';
        } else if (status === 'Pending') {
          return 'bg-red-200 text-red-800 px-3 py-1 rounded-full';
        }
        return 'bg-yellow-200 text-yellow-800 px-3 py-1 rounded-full';
      },
      openModal(action, row = null) {
        // Handle modal logic for add, edit, detail, etc.
        console.log(action, row);
      },
    },
  };
  </script>
  