---
title: "Portfolio Summary"
layout: single
permalink: /portfolio-summary/
author_profile: false
classes: wide
---

A comprehensive overview of the Weiss Schwarz collection portfolio, including inventory details and performance metrics.

---

## Inventory Summary

[📊 View Full Inventory in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pubhtml){: .btn .btn--primary}

<div id="filter-container" style="margin-bottom: 15px;">
  <input type="text" id="inventory-filter" placeholder="Filter inventory..." style="padding: 8px; width: 300px; border: 1px solid #ccc; border-radius: 4px;">
</div>

<div id="inventory-loading-message">Loading inventory data from Google Sheets...</div>
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

## Transaction Summary

[📊 View Transaction Summary in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRLK6ACEpLRx5LHGFttCLe8_0yILQZ920Mb7e0o9QybF-IfgSbMqpNDhp95IXW4lt7LDn3Or2q87Ik5/pubhtml?gid=0&single=true){: .btn .btn--primary}

<div id="transaction-loading-message">Loading transaction data from Google Sheets...</div>
<div id="transaction-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="transaction-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>Cash Flow</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody id="transaction-tbody">
    </tbody>
  </table>
</div>

---

## Portfolio Performance (IRR)

[📊 View IRR Details in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRLK6ACEpLRx5LHGFttCLe8_0yILQZ920Mb7e0o9QybF-IfgSbMqpNDhp95IXW4lt7LDn3Or2q87Ik5/pubhtml?gid=1875826057&single=true){: .btn .btn--primary}

<div id="irr-loading-message">Loading IRR data from Google Sheets...</div>
<div id="irr-error-message" style="display: none; color: red;"></div>

<div style="overflow-x: auto;">
  <table id="irr-table" style="display: none; width: 100%; white-space: nowrap;">
    <thead>
      <tr>
        <th>Date</th>
        <th>Internal Rate of Return</th>
        <th>Notes</th>
      </tr>
    </thead>
    <tbody id="irr-tbody">
    </tbody>
  </table>
</div>

<script>
// Google Sheets CSV URLs
const INVENTORY_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pub?output=csv';
const TRANSACTION_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRLK6ACEpLRx5LHGFttCLe8_0yILQZ920Mb7e0o9QybF-IfgSbMqpNDhp95IXW4lt7LDn3Or2q87Ik5/pub?gid=0&single=true&output=csv';
const IRR_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRLK6ACEpLRx5LHGFttCLe8_0yILQZ920Mb7e0o9QybF-IfgSbMqpNDhp95IXW4lt7LDn3Or2q87Ik5/pub?gid=1875826057&single=true&output=csv';

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

  if (data.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="12" style="text-align: center; font-style: italic;">No inventory records yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  data.forEach(row => {
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

// Function to populate transaction table
function populateTransactionTable(data) {
  const tbody = document.getElementById('transaction-tbody');
  tbody.innerHTML = '';

  if (data.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="3" style="text-align: center; font-style: italic;">No transaction records yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  data.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row['Cash Flow'] || ''}</td>
      <td>${row.Description || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Function to populate IRR table
function populateIRRTable(data) {
  const tbody = document.getElementById('irr-tbody');
  tbody.innerHTML = '';

  if (data.length === 0) {
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="3" style="text-align: center; font-style: italic;">No IRR records yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  data.forEach(row => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${row.Date || ''}</td>
      <td>${row['Internal Rate of Return'] || ''}</td>
      <td>${row.Notes || ''}</td>
    `;
    tbody.appendChild(tr);
  });
}

// Function to filter inventory table by search term
function filterInventoryTable(searchTerm) {
  const tbody = document.getElementById('inventory-tbody');
  const rows = tbody.getElementsByTagName('tr');
  const term = searchTerm.toLowerCase();

  Array.from(rows).forEach(row => {
    const text = row.textContent.toLowerCase();
    row.style.display = text.includes(term) ? '' : 'none';
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

    // Set up filter
    document.getElementById('inventory-filter').addEventListener('input', (e) => {
      filterInventoryTable(e.target.value);
    });
  })
  .catch(error => {
    console.error('Error loading inventory data:', error);
    document.getElementById('inventory-loading-message').style.display = 'none';
    document.getElementById('inventory-error-message').style.display = 'block';
    document.getElementById('inventory-error-message').textContent = 'Error loading inventory data: ' + error.message;
  });

// Fetch and display transaction data
fetch(TRANSACTION_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch transaction data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populateTransactionTable(data);

    // Hide loading, show table
    document.getElementById('transaction-loading-message').style.display = 'none';
    document.getElementById('transaction-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading transaction data:', error);
    document.getElementById('transaction-loading-message').style.display = 'none';
    document.getElementById('transaction-error-message').style.display = 'block';
    document.getElementById('transaction-error-message').textContent = 'Error loading transaction data: ' + error.message;
  });

// Fetch and display IRR data
fetch(IRR_CSV_URL)
  .then(response => {
    if (!response.ok) throw new Error('Failed to fetch IRR data');
    return response.text();
  })
  .then(csv => {
    const data = parseCSV(csv);
    populateIRRTable(data);

    // Hide loading, show table
    document.getElementById('irr-loading-message').style.display = 'none';
    document.getElementById('irr-table').style.display = 'table';
  })
  .catch(error => {
    console.error('Error loading IRR data:', error);
    document.getElementById('irr-loading-message').style.display = 'none';
    document.getElementById('irr-error-message').style.display = 'block';
    document.getElementById('irr-error-message').textContent = 'Error loading IRR data: ' + error.message;
  });
</script>
