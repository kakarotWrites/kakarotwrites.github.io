---
layout: post
title: "SSRF via PDF export: reading cloud metadata"
date: 2026-05-30
categories: [writeups]
tags: [SSRF, Cloud]
description: "A report generator that fetched attacker-controlled URLs."
---

## Summary

A PDF report generator fetched attacker-controlled URLs, allowing server-side requests to internal services.

![Illustration of the server-side request flow]({{ '/assets/images/ssrf-request.svg' | relative_url }})

## Impact and fix

The vulnerable service could reach internal metadata endpoints. Restrict outbound destinations, validate URLs after resolution, and block link-local and private network ranges.
