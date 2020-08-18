---
layout: default
parent: Other
grand_parent: Cheatsheets
title: Recon
nav-order: 1
---

# [](#header-1)Port Scanning

## [](#header-2)NMAP

nmap -sC -sV -O --max-rate 5000 10.10.10.82
> Tries to get service version, runs scripts, checks OS version and increases max rate to scan faster

## [](#header-2)masscan
