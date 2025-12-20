---
title: "Frieren: Beyond Journey's End"
date: 2025-12-14
categories:
  - frieren
tags:
  - weiss-schwarz
  - collection
excerpt: "Collection tracking for Frieren: Beyond Journey's End - 2 booster box cases"
classes: wide
---

## Collection Details

![Frieren]({{ site.baseurl }}/assets/images/themes/frieren.jpg)

**Date:** December 14, 2025
**Set:** Frieren: Beyond Journey's End

## Purchase History

| SKU | Quantity | Purchase Date | Price Per Unit | Price per Booster Box | Current Status | Purchase Source | Notes |
|-----|----------|---------------|----------------|-----------------------|----------------|-----------------|-------|
{%- for item in site.data.frieren.purchase-history %}
| {{ item.sku }} | {{ item.quantity }} | {{ item.purchase_date }} | {{ item.price_per_unit }} | {{ item.price_per_booster_box }} | {{ item.current_status }} | {{ item.purchase_source }} | {{ item.notes }} |
{%- endfor %}

## Sale History

Has not sold any

## Market Value

### [Booster Boxes](https://www.tcgplayer.com/product/668605/weiss-schwarz-frieren-beyond-journeys-end-frieren-beyond-journeys-end-booster-box-second-edition?Language=English)

<img src="{{ site.baseurl }}/assets/images/frieren/booster_box.jpg" alt="Booster Box" width="25%">

| Date | Market Value | Sell Through |
|------|--------------|--------------|
{%- for item in site.data.frieren.market-value-booster-boxes %}
| {{ item.date }} | {{ item.market_value }} | {{ item.sell_through }} |
{%- endfor %}

### [Booster Box Cases](https://www.tcgplayer.com/product/668606/weiss-schwarz-frieren-beyond-journeys-end-frieren-beyond-journeys-end-booster-box-case-second-edition?page=1&Language=English)

<img src="{{ site.baseurl }}/assets/images/frieren/booster_box_case.jpg" alt="Booster Box Case" width="25%">

| Date | Market Value | Sell Through |
|------|--------------|--------------|
{%- for item in site.data.frieren.market-value-booster-box-cases %}
| {{ item.date }} | {{ item.market_value }} | {{ item.sell_through }} |
{%- endfor %}

## Position Value

| Date | Asset | Quantity |
|------|-------|----------|
{%- for item in site.data.frieren.position-value %}
| {{ item.date }} | {{ item.asset }} | {{ item.quantity }} |
{%- endfor %}

Total Amount Invested : $2,178

| Date | Net Value | Net Value (Post Fees) | Rate of Return |
|------|-----------|----------------------|----------------|
{%- for item in site.data.frieren.net-value %}
| {{ item.date }} | {{ item.net_value }} | {{ item.net_value_post_fees }} | {{ item.rate_of_return }} |
{%- endfor %}
