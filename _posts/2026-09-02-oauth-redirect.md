---
layout: post
title: "From open redirect to OAuth token theft"
date: 2026-09-02
categories: [writeups]
tags: [OAuth, ATO]
description: "Chaining a loose redirect_uri check into account takeover."
---

## Summary

A loose `redirect_uri` validation allowed an open redirect to be chained into an OAuth token theft scenario.

## Impact and fix

OAuth redirect targets should be compared against an exact allowlist of registered origins and paths.
