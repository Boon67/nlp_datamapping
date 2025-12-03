# Healthcare Field Mappings System

This system provides intelligent field name matching for healthcare and insurance data standardization. It matches incoming field names against a library of known source field patterns and returns standardized target field names.

## Table Structure
- **src**: Source field name patterns (what the system matches against)
- **target**: Standardized target field name (what gets returned)

## How It Works

The system uses a two-step mapping approach:
1. **Input Matching**: Matches your input field names against known SOURCE field patterns using multiple similarity algorithms
2. **Target Return**: Returns the corresponding standardized TARGET field name for the best matching source pattern

## Field Categories Included

### Policy & Member Information
- Policy Effective Date → Policy Effective Date
- Group Name → Group Name
- Insured First Name, Last Name, DOB → Insured First Name, Insured Last Name, Insured DOB
- Claimant First Name, Last Name, DOB → Claimant First Name, Claimant Last Name, Claimant DOB

### Service & Claims Data
- Beginning/Ending Service Date → Beginning Service Date, Ending Service Date
- Processed Date → Processed Date
- Claim Number/Claim Control Number → Claim Number/Claim Control Number
- Service Line/Claim Type → Service Line/Claim Type

### Medical Coding
- Primary ICD, Secondary ICD → Primary ICD, Secondary ICD
- CPT Code, HCPCS Code → CPT Code, HCPCS Code
- Revenue Code, Modifier Code → Revenue Code, Modifier Code

### Prescription Information
- Rx Name, Quantity, Days Supply → Rx Name, Rx Quantity, Rx Days Supply
- Rx Date Filled → Rx Date Filled

### Financial Amounts
- Billed Amount, Allowed Amount, Paid Amount → Billed Amount, Allowed Amount, Paid Amount
- Copay, Deductible, Coinsurance Amount → Copay Amount, Deductible Amount, Coinsurance Amount
- Net, Ineligible, COB, Other Reduced, Denied Amount → Net Amount, Ineligible Amount, COB Amount, Other Reduced Amount, Denied Amount

### Provider Information
- NPI (National Provider Identifier) → NPI?
- Payee Name, Address, TIN → Payee Name, Payee Address, Payee TIN

## Matching Technology

The system uses multiple similarity algorithms for robust field matching:

1. **Exact Matching**: Perfect string matches after text normalization
2. **Substring Matching**: Partial matches where one field contains another
3. **Sequence Similarity**: Character-level similarity using difflib for handling typos
4. **Word Overlap**: Jaccard similarity for word-level matching
5. **TF-IDF Semantic Matching**: Vector-based semantic similarity for meaning-based matching

## Available Tools

### Python Class: FieldMatcher
- Full-featured matching with detailed scoring
- Batch processing capabilities
- Configurable confidence thresholds

### Stored Procedure: field_matcher_advanced()
- Production-ready SQL interface
- Returns detailed match scores and rankings
- Supports multiple input fields at once

### Simple Function: field_matcher_predict_simple()
- Quick single-field matching
- Returns best match above threshold
- Lightweight for simple use cases

## Usage

The matching system will automatically map incoming healthcare field names to standardized target field names, enabling consistent data processing across different healthcare data sources regardless of how the original fields were named.

**Example**: 
- Input: "Patient First Name" → Output: "Insured First Name"
- Input: "DOB" → Output: "Insured DOB"  
- Input: "Claim ID" → Output: "Claim Number/Claim Control Number"
