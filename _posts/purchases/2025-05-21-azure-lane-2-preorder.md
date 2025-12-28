---
title: "Purchase: Azure Lane Preorders"
date: 2025-12-13
categories:
  - purchases
excerpt: "All preorders done for azure lane 2"
classes: wide
---

## Purchase Details

![Azure Lane 2]({{ site.baseurl }}/assets/images/themes/azurelane2.jpg)

**Date:** May 21, 2025

Content coming soon...

## Purchase History

<div id="filter-container" style="margin-bottom: 15px;">
  <input type="text" id="table-filter" placeholder="Filter table..." style="padding: 8px; width: 300px; border: 1px solid #ccc; border-radius: 4px;">
</div>

<div id="loading-message">Loading data from Google Sheets...</div>
<div id="error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="purchase-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>SKU</th>
        <th>Description</th>
        <th>Broken Down Unit</th>
        <th>Quantity</th>
        <th>Purchase Price</th>
        <th>Price Per Unit</th>
        <th>Purchase Source</th>
        <th>Last Checked Date</th>
        <th>Last Checked Status</th>
      </tr>
    </thead>
    <tbody id="purchase-tbody">
    </tbody>
  </table>
</div>

<script>
// Google Sheets CSV URL
const SHEET_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSWj6XOTy5jj69GOaUswg7CaeglVadPyzA1yTkJOO1UDe3wukvHMy6ivsAugLNxb5iQgAbzxqPDtOSr/pub?output=csv';

// Default filter - only show this set
const DEFAULT_SET_FILTER = 'Azure Lane';

// Store all data for filtering
let allData = [];

// Function to parse CSV data with proper quote handling
function parseCSV(csv) {
  const lines = csv.trim().split('\n');
  const data = [];

  // Parse a single CSV line handling quoted fields
  function parseLine(line) {
    const result = [];
    let current = '';
    let inQuotes = false;

    for (let i = 0; i < line.length; i++) {
      const char = line[i];
      const nextChar = line[i + 1];

      if (char === '"') {
        if (inQuotes && nextChar === '"') {
          // Escaped quote
          current += '"';
          i++;
        } else {
          // Toggle quote state
          inQuotes = !inQuotes;
        }
      } else if (char === ',' && !inQuotes) {
        // Field separator
        result.push(current.trim());
        current = '';
      } else {
        current += char;
      }
    }

    // Add last field
    result.push(current.trim());
    return result;
  }

  // Parse headers
  const headers = parseLine(lines[0]);

  // Parse data rows
  for (let i = 1; i < lines.length; i++) {
    const values = parseLine(lines[i]);
    const row = {};
    headers.forEach((header, index) => {
      row[header] = values[index] || '';
    });
    data.push(row);
  }

  return data;
}

// Function to populate table with optional set filtering
function populateTable(data, filterBySet = true) {
  const tbody = document.getElementById('purchase-tbody');
  tbody.innerHTML = '';

  // Filter by set if enabled
  const filteredData = filterBySet
    ? data.filter(row => {
        const set = row.Set || row.set || '';
        return set.includes(DEFAULT_SET_FILTER);
      })
    : data;

  filteredData.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row.SKU || ''}</td>
      <td>${row.Description || ''}</td>
      <td>${row['Broken Down Unit'] || ''}</td>
      <td>${row.Quantity || ''}</td>
      <td>${row['Purchase Price'] || ''}</td>
      <td>${row['Price Per Broken Down Unit'] || ''}</td>
      <td>${row['Purchase Source'] || ''}</td>
      <td>${row['Last Checked Date'] || ''}</td>
      <td>${row['Last Checked Status'] || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Function to filter table by search term
function filterTable(searchTerm) {
  const tbody = document.getElementById('purchase-tbody');
  const rows = tbody.getElementsByTagName('tr');
  const term = searchTerm.toLowerCase();

  Array.from(rows).forEach(row => {
    const text = row.textContent.toLowerCase();
    row.style.display = text.includes(term) ? '' : 'none';
  });
}

// Fetch and display data
fetch(SHEET_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch data');
    return response.text();
  })
  .then(csv => {
    console.log('Raw CSV:', csv); // Debug: see raw CSV
    allData = parseCSV(csv);
    console.log('Parsed data:', allData); // Debug: see parsed data
    console.log('Total rows:', allData.length); // Debug: row count

    // Populate table with default set filter applied
    populateTable(allData, true);

    // Check if any rows are displayed
    const displayedRows = document.querySelectorAll('#purchase-tbody tr').length;
    console.log('Displayed rows after filter:', displayedRows); // Debug: filtered row count

    // Hide loading, show table
    document.getElementById('loading-message').style.display = 'none';
    document.getElementById('purchase-table').style.display = 'table';
    document.getElementById('purchase-table').parentElement.style.display = 'block';

    // Show warning if no rows after filtering
    if (displayedRows === 0) {
      const errorDiv = document.getElementById('error-message');
      errorDiv.style.display = 'block';
      errorDiv.style.color = 'orange';
      errorDiv.textContent = `Data loaded (${allData.length} total rows), but no rows match filter "${DEFAULT_SET_FILTER}". Check browser console for details.`;
    }

    // Set up filter
    document.getElementById('table-filter').addEventListener('input', (e) => {
      filterTable(e.target.value);
    });
  })
  .catch(error => {
    console.error('Error loading data:', error);
    document.getElementById('loading-message').style.display = 'none';
    document.getElementById('error-message').style.display = 'block';
    document.getElementById('error-message').textContent = 'Error loading data: ' + error.message + '. Please check the CSV URL.';
  });
</script>

## Receipts
![N4Y TCG Receipt]({{ site.baseurl }}/assets/images/receipts/2025/n4y-tcg-azure.jpg)
![Goldstar Receipt]({{ site.baseurl }}/assets/images/receipts/2025/goldstar-azure.jpg)
![Lumius Receipt]({{ site.baseurl }}/assets/images/receipts/2025/lumius-azure.jpg)