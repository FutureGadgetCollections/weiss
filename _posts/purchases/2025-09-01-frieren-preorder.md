---
title: "Purchase: Frieren  Preorders"
date: 2025-09-01
categories:
  - purchases
excerpt: "All preorders done for Frieren"
classes: wide
---

## Purchase Details

![Frieren]({{ site.baseurl }}/assets/images/themes/frieren.jpg)

**Date:** September 01, 2025


## Purchase History

| SKU | Quantity | Purchase Date | Price Per Unit | Price per Booster Box | Current Status | Purchase Source | Notes |
|-----|----------|---------------|----------------|-----------------------|----------------|-----------------|-------|
{%- for item in site.data.frieren.purchase-history %}
| {{ item.sku }} | {{ item.quantity }} | {{ item.purchase_date }} | {{ item.price_per_unit }} | {{ item.price_per_booster_box }} | {{ item.current_status }} | {{ item.purchase_source }} | {{ item.notes }} |
{%- endfor %}

## Receipts

![Goldstar Receipt](receipts/2025/goldstar-frieren.jpg)