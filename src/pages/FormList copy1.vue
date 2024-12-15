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
        <tr class="hover:bg-gray-50">
          <td class="border px-4 py-2">1</td>
          <td class="border px-4 py-2">CMT-PR2412.0003</td>
          <td class="border px-4 py-2">2024-12-06</td>
          <td class="border px-4 py-2">2024-12-14</td>
          <td class="border px-4 py-2">Kumatsu-01</td>
          <td class="border px-4 py-2">For Head work</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">KEAT Khoun</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">
            <span
              class="bg-yellow-200 text-yellow-800 px-3 py-1 rounded-full"
            >
               Approve
            </span>
          </td>
          <td class="border px-4 py-2 flex space-x-2">
            <button title="Edit">
              <i class="fas fa-edit text-blue-500"></i>
            </button>
            <button title="Delete">
              <i class="fas fa-trash-alt text-red-500"></i>
            </button>
            <button title="Details">
              <i class="fas fa-file-alt text-gray-500"></i>
            </button>
            <button title="Print">
              <i class="fas fa-print text-gray-500"></i>
            </button>
          </td>
        </tr>

        <tr class="hover:bg-gray-50">
          <td class="border px-4 py-2">2</td>
          <td class="border px-4 py-2">CMT-PR2412.0003</td>
          <td class="border px-4 py-2">2024-12-06</td>
          <td class="border px-4 py-2">2024-12-14</td>
          <td class="border px-4 py-2">Kumatsu-01</td>
          <td class="border px-4 py-2">For Head work</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">KEAT Khoun</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">
            <span
              class="bg-red-200 text-yellow-800 px-3 py-1 rounded-full"
            >
               Pending
            </span>
          </td>
          <td class="border px-4 py-2 flex space-x-2">
            <button title="Edit">
              <i class="fas fa-edit text-blue-500"></i>
            </button>
            <button title="Delete">
              <i class="fas fa-trash-alt text-red-500"></i>
            </button>
            <button title="Details">
              <i class="fas fa-file-alt text-gray-500"></i>
            </button>
            <button title="Print">
              <i class="fas fa-print text-gray-500"></i>
            </button>
          </td>
        </tr>
        
        <tr class="hover:bg-gray-50">
          <td class="border px-4 py-2">3</td>
          <td class="border px-4 py-2">CMT-PR2412.0003</td>
          <td class="border px-4 py-2">2024-12-06</td>
          <td class="border px-4 py-2">2024-12-14</td>
          <td class="border px-4 py-2">Kumatsu-01</td>
          <td class="border px-4 py-2">For Head work</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">YUN Tola</td>
          <td class="border px-4 py-2">KEAT Khoun</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">
            <span
              class="bg-red-200 text-yellow-800 px-3 py-1 rounded-full"
            >
               Pending
            </span>
          </td>
          <td class="border px-4 py-2 flex space-x-2">
            <button title="Edit">
              <i class="fas fa-edit text-blue-500"></i>
            </button>
            <button title="Delete">
              <i class="fas fa-trash-alt text-red-500"></i>
            </button>
            <button title="Details">
              <i class="fas fa-file-alt text-gray-500"></i>
            </button>
            <button title="Print">
              <i class="fas fa-print text-gray-500"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>


  </template>
  
  <script>
  export default {
    data() {
      return {
        rows: [
          {
            id: 1,
            pr_id: "CMT-PR2412-0003",
            request_date: "2024-12-06",
            due_date: "2024-12-14",
            purpose: "Purpose 1",
            status: "Pending",
          },
          {
            id: 2,
            pr_id: "CMT-PR2412-0004",
            request_date: "2024-12-06",
            due_date: "2024-12-14",
            purpose: "Purpose 2",
            status: "Approved",
          },
        ],
      };
    },
  };
  </script>
  