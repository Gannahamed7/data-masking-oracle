# data-masking-oracle
# UAT Data Masking & Anonymization System

## Overview
This repository contains an Oracle PL/SQL pipeline designed to anonymize and mask sensitive customer data for User Acceptance Testing (UAT) environments. It generates realistic, structurally accurate test datasets to support secure software testing without exposing actual production data. 

The pipeline ensures data consistency and compliance with secure enterprise and banking data handling practices by irreversibly transforming Personally Identifiable Information (PII) before it reaches non-production environments.

## Features
* **Data Masking:** Partially redacts highly sensitive strings (e.g., masking Payment Card numbers to display only the first and last 4 digits).
* **Data Substitution:** Replaces real names, physical addresses, and email addresses with realistic, randomly assigned dummy data using predefined lookup tables.
* **Procedural Generation:** Algorithmically generates mathematically valid, localized data points, including 14-digit Egyptian National IDs and 11-digit Egyptian mobile phone numbers.
* **Data Scrambling (Permutation):** Shuffles and modifies existing numeric strings (such as Account Numbers) using positional swapping and modulo arithmetic to destroy the original identity while maintaining the exact string length and format.
* **Referential Integrity:** Preserves database architecture by acting directly on ROWIDs and maintaining Primary Key / Unique constraints during the transformation process.

## Technologies Used
* **Language:** Oracle PL/SQL
* **Domains:** Database Security, Data Masking, Data Obfuscation, Compliance

## How It Works
1. **Environment Setup:** The script drops existing mock tables and rebuilds the `MYDATA2` target table alongside several lookup tables (`NAMES`, `CITIES`, `STREET_NAMES`, etc.).
2. **Execution:** A series of modular PL/SQL functions and procedures (`fake_name`, `mask_card`, `fake_national_id`, etc.) are executed in a batch block.
3. **Randomization:** The procedures utilize `DBMS_RANDOM.VALUE` to assign randomized but structurally realistic values to every row in the target table.

## Security Disclaimer
**This script is intended strictly for use in non-production (UAT, QA, DEV) environments.** 
The anonymization techniques used here (substitution and obfuscation) are destructive by design. Running this script overwrites existing data and cannot be reversed. It does not employ reversible cryptographic encryption; it is meant to sanitize databases completely to prevent compliance breaches during the software testing lifecycle.
