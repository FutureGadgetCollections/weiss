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

| SKU | Quantity | Purchase Date | Price Per Unit | Price per Booster Box | Current Status | Purchase Source | Notes |
|-----|----------|---------------|----------------|-----------------------|----------------|-----------------|-------|
{%- for item in site.data.azur-lane-2.purchase-history %}
| {{ item.sku }} | {{ item.quantity }} | {{ item.purchase_date }} | {{ item.price_per_unit }} | {{ item.price_per_booster_box }} | {{ item.current_status }} | {{ item.purchase_source }} | {{ item.notes }} |
{%- endfor %}


## Receipts
![N4Y TCG Receipt](receipts/2025/n4y-tcg-azure.jpg)
![Goldstar Receipt](receipts/2025/goldstar-azure.jpg)
![Lumius Receipt](receipts/2025/lumius-azure.jpg)