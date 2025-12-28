---
title: "All Collections"
layout: single
permalink: /collection/
author_profile: false
classes: wide
---

Welcome to the Weiss Schwarz collection showcase!

## Inventory Summary

[📊 View Full Inventory in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pubhtml){: .btn .btn--primary}

<div id="filter-container" style="margin-bottom: 15px;">
  <input type="text" id="table-filter" placeholder="Filter inventory..." style="padding: 8px; width: 300px; border: 1px solid #ccc; border-radius: 4px;">
</div>

<div id="loading-message">Loading inventory data from Google Sheets...</div>
<div id="error-message" style="display: none; color: red;"></div>

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

<script>
// Google Sheets CSV URL
const SHEET_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRBKSsmO2hnPiozvmN80qtqxSqQUkZQv00znssNO_8HUy4TULbVTcQI0SqieoGBofWm4EjEJv-P2jjE/pub?output=csv';

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

// Function to populate table
function populateTable(data) {
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

// Function to filter table by search term
function filterTable(searchTerm) {
  const tbody = document.getElementById('inventory-tbody');
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
    allData = parseCSV(csv);

    // Populate table with all data (no filtering)
    populateTable(allData);

    // Hide loading, show table
    document.getElementById('loading-message').style.display = 'none';
    document.getElementById('inventory-table').style.display = 'table';
    document.getElementById('inventory-table').parentElement.style.display = 'block';

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

---

## Weiss Schwarz Sets

<div class="feature__wrapper">
  <div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-teaser">
        <img src="{{ site.baseurl }}/assets/images/themes/makeine.jpg" alt="Too Many Losing Heroines">
      </div>
      <div class="archive__item-body">
        <h3 class="archive__item-title"><a href="{{ site.baseurl }}/collection/too-many-losing-heroines/">Too Many Losing Heroines</a></h3>
        <p class="archive__item-excerpt">Weiss Schwarz cards from the Too Many Losing Heroines set</p>
      </div>
    </div>
  </div>

  <div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-teaser">
        <img src="{{ site.baseurl }}/assets/images/themes/azurelane2.jpg" alt="Azur Lane 2">
      </div>
      <div class="archive__item-body">
        <h3 class="archive__item-title"><a href="{{ site.baseurl }}/collection/azure-lane-2/">Azure Lane 2</a></h3>
        <p class="archive__item-excerpt">Weiss Schwarz cards from the Azure Lane 2 set</p>
      </div>
    </div>
  </div>

  <div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-teaser">
        <img src="{{ site.baseurl }}/assets/images/themes/frieren.jpg" alt="Frieren">
      </div>
      <div class="archive__item-body">
        <h3 class="archive__item-title"><a href="{{ site.baseurl }}/collection/frieren/">Frieren</a></h3>
        <p class="archive__item-excerpt">Weiss Schwarz cards from the Frieren set</p>
      </div>
    </div>
  </div>
</div>

---

*Use the navigation menu above to jump directly to any collection.*
