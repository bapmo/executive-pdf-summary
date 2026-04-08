# Executive PDF Summarization

**Version:** 1.0

## Overview
The Executive PDF Summarization skill processes a text-based PDF document and generates a concise, executive-ready summary in bullet-point format. It preserves key information without hallucination and constrains output length to 1–3 pages for efficient decision-making.

This skill is ideal for executives, analysts, or anyone needing a high-level summary of medium-to-large PDF reports.

---

## When to Use
- When a readable (text-based) PDF is provided
- When an executive summary is required for meetings or briefings
- When extracting key insights, decisions, risks, or highlights from medium-to-large documents

## Do Not Use When
- The PDF is scanned or image-based with no extractable text
- The document is very short (<500 words)
- Full-detail fidelity is required (e.g., legal review, contracts, compliance analysis)

---

## Features
- Extracts text from readable PDFs
- Identifies document structure (headings, sections)
- Extracts key insights: decisions, metrics, risks, conclusions
- Synthesizes concise bullet-point summaries
- Validates output for clarity and semantic consistency
- Provides retry logic if output fails validation

---

## How It Works

### Steps:
1. **Validate Input**  
   - Ensure the PDF is readable and text-based  
   - Return error if unreadable or empty

2. **Extract Text**  
   - Extract full text from PDF  
   - Notify user if extraction fails

3. **Assess Document Size**  
   - Determine word count and apply summary length rules:  
     - 500–5,000 words → 1 page  
     - 5,001–25,000 words → 2 pages  
     - 25,001–50,000 words → 3 pages

4. **Analyze Content**  
   - Identify document structure  
   - Extract key points: decisions, metrics, risks, conclusions

5. **Synthesize Summary**  
   - Convert insights into concise bullet points  
   - Preserve original meaning; do not introduce new information

6. **Validate Output**  
   - Check syntax, clarity, completeness  
   - Check semantic consistency  
   - Trigger retry logic if validation fails

7. **Format Output**  
   - Structure bullet points for executive readability  
   - Deliver editable text output

---

### Retry Logic
- On semantic or structural validation failure:  
  1. Retry synthesis with stricter constraints (top-priority points only)  
  2. Reduce verbosity and re-validate  
  3. If validation fails again: output with warning:  
    > "Summary may be incomplete or ambiguous due to source document complexity"

---

## Example

**Input:** PDF containing a quarterly business report  

**Output:**
- Revenue increased by 18% compared to last quarter  
- Expansion into UAE and Germany markets  
- Operational costs rose by 6% due to hiring  
- Key risk: supply chain delays expected in Q3  
- Recommendation: optimize vendor contracts  

---

## Limitations
- Does not support scanned/image-based PDFs (no OCR)  
- Cannot process password-protected files  
- May lose nuance in highly technical or dense documents  
- Assumes reasonably structured input text  
- Not suitable for tasks requiring full detail preservation

---

## Usage (Python Example)

```python
from executive_pdf_summary import summarize_pdf

summary = summarize_pdf("quarterly_report.pdf")
print(summary)
