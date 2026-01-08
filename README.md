
# Document Processing & Archival Agent (Archive Intelligence)

A MindStudio AI agent that automatically processes PDF documents from email attachments, cleans up OCR text, and organizes documents with structured metadata.

## Summary
<p align="left">
  <img src="assets/archivist%20promo.gif" width="450" alt="Archivist promo demo" />
</p>


## Rationale

Managing document archives often involves tedious manual work:
- Extracting text from scanned documents
- Cleaning up OCR artifacts and formatting issues
- Creating searchable document versions
- Maintaining consistent metadata
- Building a searchable index of documents

This agent automates the entire workflow, transforming unstructured documents into a well-organized digital archive with minimal human intervention.

## Features & Technology Stack

### Features
- **Email-triggered processing**: Send documents via email and they're automatically processed
- **OCR cleanup**: Removes artifacts, fixes line breaks, and improves text quality
- **Dual storage**: Creates both raw and cleaned versions for reference
- **Intelligent metadata extraction**: Automatically identifies document type, author, date, source, etc.
- **Centralized tracking**: Updates a Google Sheet with document metadata and links

### Technology Stack
- **MindStudio** for workflow orchestration
- **Gemini 2.0 Flash Lite** for underlying model and text cleaning
- **Claude 3 Haiku** for metadata extraction
- **Google Docs API** for document storage
- **Google Sheets API** for metadata indexing
- **JavaScript** custom function for data transformation (vibe-coded in MindStudio)

## Sample Output

When an email with subject "006" and a PDF attachment is processed:

1. **Text Extraction & Cleaning**
   - Extracts raw OCR text from PDF
   - Removes artifacts and improves formatting

2. **Document Creation**
   - Creates "006_CLEAN.docx" with cleaned text
   - Creates "006_RAW.docx" with original OCR text

3. **Metadata Generation**
   ```json
   [
     {
       "document_id": "006",
       "document_type": "Email",
       "author_or_speaker": "Ligaya Beebe",
       "date_or_date_range": "May 8, 1994",
       "institution_or_source": "Agency for International Development",
       "notes": "Email regarding EER (Employee Evaluation Report) work requirements...",
       "cleanURL": "https://docs.google.com/document/d/...",
       "rawURL": "https://docs.google.com/document/d/..."
     }
   ]
   ```

4. **Metadata Storage**
   - Updates Google Sheet with new entry in CSV format
   - Includes document ID, type, author, date, and document links

## Limitations

- **Document Types**: Currently only processes PDF attachments
- **Authentication**: Requires Google Workspace integration and permissions
- **Security**: Only processes emails from approved senders
- **Document ID**: Uses email subject as document ID, requiring consistent subject line formatting
- **OCR Quality**: Final output dependent on initial OCR quality in the PDF

## Setup & Usage

1. Deploy the MindStudio agent to your workspace [Remix Link](https://app.mindstudio.ai/agents/archive-intelligence-a1fcd0dc/remix)
2. Configure Live Trigger Email and Google Workspace integration with appropriate permissions
3. Add approved email sender addresses
4. Send emails with PDF attachments using the document ID as the subject line
5. Access organized documents in Google Drive and view the metadata index in Google Sheets

---

*Built with [MindStudio](https://mindstudio.ai) - AI Agents for the Enterprise*
