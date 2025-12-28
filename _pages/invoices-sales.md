---
title: "Sales"
layout: archive
permalink: /invoices/sales/
author_profile: false
classes: wide
---

All sale transactions for the WEISS collection.

[📊 View Full Sales Data in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vSZuEpbE6MRD1vLNdpQx6e4SrAsiqAUuP5ywUWuSf2vmpBs_9nIEP4u66Z87nAvLbGEcIk0-wUVD_MQ/pubhtml){: .btn .btn--primary}

## Sales Summary

<div id="filter-container" style="margin-bottom: 15px;">
  <input type="text" id="table-filter" placeholder="Filter table..." style="padding: 8px; width: 300px; border: 1px solid #ccc; border-radius: 4px;">
</div>

<div id="loading-message">Loading sales data from Google Sheets...</div>
<div id="error-message" style="display: none; color: red;"></div>

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

<script>
// Google Sheets CSV URL
const SHEET_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSZuEpbE6MRD1vLNdpQx6e4SrAsiqAUuP5ywUWuSf2vmpBs_9nIEP4u66Z87nAvLbGEcIk0-wUVD_MQ/pub?output=csv';

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
  const tbody = document.getElementById('sales-tbody');
  tbody.innerHTML = '';

  if (data.length === 0) {
    // Show "no sales yet" message in table
    const tr = document.createElement('tr');
    tr.innerHTML = '<td colspan="9" style="text-align: center; font-style: italic;">No sale records yet.</td>';
    tbody.appendChild(tr);
    return;
  }

  data.forEach(row => {
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

// Function to filter table by search term
function filterTable(searchTerm) {
  const tbody = document.getElementById('sales-tbody');
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
    document.getElementById('sales-table').style.display = 'table';
    document.getElementById('sales-table').parentElement.style.display = 'block';

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

## Sale Details by Transaction

{% assign sale_posts = site.categories.sales %}
{% if sale_posts.size > 0 %}
  {% assign posts_by_year = sale_posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in posts_by_year %}

## {{ year.name }}

{% for post in year.items reversed %}
      {% include archive-single.html %}
    {% endfor %}
  {% endfor %}
{% else %}
  *No sale records yet.*
{% endif %}
