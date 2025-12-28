---
title: "Too Many Losing Heroines"
layout: single
permalink: /collection/too-many-losing-heroines/
taxonomy: too-many-losing-heroines
author_profile: false
classes: wide
---

![Too Many Losing Heroines]({{ site.baseurl }}/assets/images/themes/makeine.jpg)

Weiss Schwarz cards from the Too Many Losing Heroines set.

---

## My Thoughts and Research

- [Entry Research: Too Many Losing Heroines]({{ site.baseurl }}/research/tmlh-entry-research/)
- [English Release Research: Too Many Losing Heroines]({{ site.baseurl }}/research/tmlh-english-release-research/)

---

## Current Collection

[📊 View Full Inventory in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pubhtml){: .btn .btn--primary}

<div id="inventory-loading-message">Loading current collection data...</div>
<div id="inventory-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="inventory-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Last Checked Date</th>
        <th>Status</th>
        <th>Set</th>
        <th>SKU</th>
        <th>Description</th>
        <th>Broken Down Unit</th>
        <th>Quantity</th>
        <th>Market Value</th>
        <th>Market Value (Per Unit)</th>
        <th>Purchase Date</th>
        <th>Purchase Price</th>
        <th>Price Per Unit</th>
      </tr>
    </thead>
    <tbody id="inventory-tbody">
    </tbody>
  </table>
</div>

---

## Purchase History

[📊 View Full Purchase Data in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vSWj6XOTy5jj69GOaUswg7CaeglVadPyzA1yTkJOO1UDe3wukvHMy6ivsAugLNxb5iQgAbzxqPDtOSr/pubhtml){: .btn .btn--primary}

<div id="purchase-loading-message">Loading purchase history...</div>
<div id="purchase-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="purchase-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>Set</th>
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

---

## Sales History

[📊 View Full Sales Data in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vSZuEpbE6MRD1vLNdpQx6e4SrAsiqAUuP5ywUWuSf2vmpBs_9nIEP4u66Z87nAvLbGEcIk0-wUVD_MQ/pubhtml){: .btn .btn--primary}

<div id="sales-loading-message">Loading sales history...</div>
<div id="sales-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="sales-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>Set</th>
        <th>SKU</th>
        <th>Description</th>
        <th>Quantity</th>
        <th>Purchase Date</th>
        <th>Purchase Price</th>
        <th>Sale Price</th>
        <th>Sale Source</th>
      </tr>
    </thead>
    <tbody id="sales-tbody">
    </tbody>
  </table>
</div>

---

## Performance Tracking

[📊 View Market Research Data in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vQyC5B5pYQEuhr7PZ2fZI1SwnbuLh0Aryro3hRta_QMFxYS7j82-B3ftabBcwTOpoHn2-l4QgB1qlVj/pubhtml?gid=0&single=true){: .btn .btn--primary}

<div id="market-loading-message">Loading market research data...</div>
<div id="market-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="market-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>Sale Price</th>
        <th>Selling Throughput</th>
        <th>Rate of Return on Investment</th>
      </tr>
    </thead>
    <tbody id="market-tbody">
    </tbody>
  </table>
</div>

<script>
// Google Sheets CSV URLs
const INVENTORY_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pub?output=csv';
const PURCHASE_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSWj6XOTy5jj69GOaUswg7CaeglVadPyzA1yTkJOO1UDe3wukvHMy6ivsAugLNxb5iQgAbzxqPDtOSr/pub?output=csv';
const SALES_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSZuEpbE6MRD1vLNdpQx6e4SrAsiqAUuP5ywUWuSf2vmpBs_9nIEP4u66Z87nAvLbGEcIk0-wUVD_MQ/pub?output=csv';
const MARKET_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQyC5B5pYQEuhr7PZ2fZI1SwnbuLh0Aryro3hRta_QMFxYS7j82-B3ftabBcwTOpoHn2-l4QgB1qlVj/pub?gid=0&single=true&output=csv';

// Set filter
const SET_FILTER = 'Too Many Losing Heiroines(JPN)';

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

// Function to populate inventory table
function populateInventoryTable(data) {
  const tbody = document.getElementById('inventory-tbody');
  tbody.innerHTML = '';

  // Filter data by set
  const filteredData = data.filter(row => row.Set === SET_FILTER);

  if (filteredData.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="12" style="text-align: center; font-style: italic;">No inventory records for this set yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  filteredData.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row['Last Checked Date'] || ''}</td>
      <td>${row.Status || ''}</td>
      <td>${row.Set || ''}</td>
      <td>${row.SKU || ''}</td>
      <td>${row.Description || ''}</td>
      <td>${row['Broken Down Unit'] || ''}</td>
      <td>${row.Quantity || ''}</td>
      <td>${row['Market Value'] || ''}</td>
      <td>${row['Market Value (Broken Down Unit)'] || ''}</td>
      <td>${row['Purchase Date'] || ''}</td>
      <td>${row['Purchase Price'] || ''}</td>
      <td>${row['Price Per Broken Down Unit'] || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Function to populate purchase table
function populatePurchaseTable(data) {
  const tbody = document.getElementById('purchase-tbody');
  tbody.innerHTML = '';

  // Filter data by set
  const filteredData = data.filter(row => row.Set === SET_FILTER);

  if (filteredData.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="11" style="text-align: center; font-style: italic;">No purchase records for this set yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  filteredData.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row.Set || ''}</td>
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

// Function to populate sales table
function populateSalesTable(data) {
  const tbody = document.getElementById('sales-tbody');
  tbody.innerHTML = '';

  // Filter data by set
  const filteredData = data.filter(row => row.Set === SET_FILTER);

  if (filteredData.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="9" style="text-align: center; font-style: italic;">No sale records for this set yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  filteredData.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row.Set || ''}</td>
      <td>${row.SKU || ''}</td>
      <td>${row.Description || ''}</td>
      <td>${row.Quantity || ''}</td>
      <td>${row['Purchase Date'] || ''}</td>
      <td>${row['Purchase Price'] || ''}</td>
      <td>${row['Sale Price'] || ''}</td>
      <td>${row['Sale Source'] || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Function to populate market research table
function populateMarketTable(data) {
  const tbody = document.getElementById('market-tbody');
  tbody.innerHTML = '';

  if (data.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="4" style="text-align: center; font-style: italic;">No market research data yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  data.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row['Sale Price'] || ''}</td>
      <td>${row['Selling Throughput'] || ''}</td>
      <td>${row['Rate of Return on Investment'] || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Fetch and display inventory data
fetch(INVENTORY_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch inventory data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populateInventoryTable(data);

    // Hide loading, show table
    document.getElementById('inventory-loading-message').style.display = 'none';
    document.getElementById('inventory-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading inventory data:', error);
    document.getElementById('inventory-loading-message').style.display = 'none';
    document.getElementById('inventory-error-message').style.display = 'block';
    document.getElementById('inventory-error-message').textContent = 'Error loading inventory data: ' + error.message;
  });

// Fetch and display purchase data
fetch(PURCHASE_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch purchase data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populatePurchaseTable(data);

    // Hide loading, show table
    document.getElementById('purchase-loading-message').style.display = 'none';
    document.getElementById('purchase-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading purchase data:', error);
    document.getElementById('purchase-loading-message').style.display = 'none';
    document.getElementById('purchase-error-message').style.display = 'block';
    document.getElementById('purchase-error-message').textContent = 'Error loading purchase data: ' + error.message;
  });

// Fetch and display sales data
fetch(SALES_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch sales data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populateSalesTable(data);

    // Hide loading, show table
    document.getElementById('sales-loading-message').style.display = 'none';
    document.getElementById('sales-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading sales data:', error);
    document.getElementById('sales-loading-message').style.display = 'none';
    document.getElementById('sales-error-message').style.display = 'block';
    document.getElementById('sales-error-message').textContent = 'Error loading sales data: ' + error.message;
  });

// Fetch and display market research data
fetch(MARKET_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch market research data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populateMarketTable(data);

    // Hide loading, show table
    document.getElementById('market-loading-message').style.display = 'none';
    document.getElementById('market-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading market research data:', error);
    document.getElementById('market-loading-message').style.display = 'none';
    document.getElementById('market-error-message').style.display = 'block';
    document.getElementById('market-error-message').textContent = 'Error loading market research data: ' + error.message;
  });
</script>
