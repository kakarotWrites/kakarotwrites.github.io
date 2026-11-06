---
layout: post
title: "IDOR in a billing API led to full invoice exposure"
date: 2026-10-14
categories: [writeups]
tags: [IDOR, API]
description: "How changing one numeric ID exposed other customers’ invoices, and how the fix was verified."
---

## Summary

Changing one numeric invoice ID exposed another customer’s invoice because the API did not verify ownership.

![Illustration of the vulnerable invoice request]({{ '/assets/images/idor-request.svg' | relative_url }})

## Steps to reproduce

1. Create or use an account with permission to view an invoice.
2. Change the invoice identifier in the request.
3. Confirm that a different customer’s invoice is returned.

Redact tokens and customer data from published evidence.

## Impact and fix

An attacker could read other customers’ invoices. The fix must enforce authorization against the authenticated account on every invoice lookup.
