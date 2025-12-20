---
title: "Portfolio Summary: December 2025"
date: 2025-12-14
categories:
  - portfolio-summary
tags:
  - portfolio
excerpt: "December 2025"
classes: wide
---

## Portfolio Overview

| Date | Cost Basis | Current Value | Fire Sale Value (85%) | ROI |
|------|------------|---------------|----------------------|-----|
{%- for item in site.data.portfolio-summary.portfolio-overview %}
| {{ item.date }} | {{ item.cost_basis }} | {{ item.current_value }} | {{ item.fire_sale_value }} | {{ item.roi }} |
{%- endfor %}

## Realized Profits

| Date Captured | Realized Profit Since Last Capture |
|---------------|-----------------------------------|
{%- for item in site.data.portfolio-summary.realized-profits %}
| {{ item.date_captured }} | {{ item.realized_profit }} |
{%- endfor %}
