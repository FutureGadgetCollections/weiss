---
title: "Azure Lane 2 Collection Details"
date: 2025-12-14
categories:
  - azure-lane-2
tags:
  - weiss-schwarz
  - collection
excerpt: "Collection tracking for Azure Lane Vol. 2 - 4 booster box cases (including 1 master case)"
classes: wide
---

## Azur Lane Vol. 2

![azure]({{ site.baseurl }}/assets/images/themes/azurelane2.jpg)

**Date:** December 14, 2025
**Set:** Azur Lane Vol. 2

## Purchase History

| SKU | Quantity | Purchase Date | Price Per Unit | Price per Booster Box | Current Status | Purchase Source | Notes |
|-----|----------|---------------|----------------|-----------------------|----------------|-----------------|-------|
{% for item in site.data.azur-lane-2.purchase-history -%}							
| {{ item.sku }} | {{ item.quantity }} | {{ item.purchase_date }} | {{ item.price_per_unit }} | {{ item.price_per_booster_box }} | {{ item.current_status }} | {{ item.purchase_source }} | {{ item.notes }} |
{% endfor %}

## Sale History

Has not sold any

## Market Value

### [Booster Boxes](https://www.tcgplayer.com/product/646335/weiss-schwarz-azur-lane-vol-2-azur-lane-vol-2-booster-box?page=1&Language=English)

<img src="{{ site.baseurl }}/assets/images/azur-lane-2/booster_box.jpg" alt="Booster Box" width="25%">

| Date | Market Value | Sell Through |
|------|--------------|--------------|
{%- for item in site.data.azur-lane-2.market-value-booster-boxes %}
| {{ item.date }} | {{ item.market_value }} | {{ item.sell_through }} |
{%- endfor %}

### [Booster Box Cases](https://www.tcgplayer.com/product/646343/weiss-schwarz-azur-lane-vol-2-azur-lane-vol-2-booster-box-case?page=1&Language=English)

<img src="{{ site.baseurl }}/assets/images/azur-lane-2/booser_case.jpg" alt="Booster Box Case" width="25%">

| Date | Market Value | Sell Through |
|------|--------------|--------------|
{%- for item in site.data.azur-lane-2.market-value-booster-box-cases %}
| {{ item.date }} | {{ item.market_value }} | {{ item.sell_through }} |
{%- endfor %}

## Position Value

| Date | Asset | Quantity |
|------|-------|----------|
{%- for item in site.data.azur-lane-2.position-value %}
| {{ item.date }} | {{ item.asset }} | {{ item.quantity }} |
{%- endfor %}

Total Amount Invested : $4278


| Date | Net Value | Net Value (Post Fees) | Rate of Return | Rate of Return (Post Fees) |
|------|-----------|-----------------------|----------------|----------------------------|
{% for item in site.data.azur-lane-2.net-value -%}
| {{ item.date }} | {{ item.net_value }} | {{ item.net_value_post_fees }} | {{ item.rate_of_return }} | {{ item.rate_of_return_post_fees }} |
{% endfor -%}

