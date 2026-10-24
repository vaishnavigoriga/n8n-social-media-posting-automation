# AI News Social Media Automation with n8n

## The solution

This n8n workflow turns AI news articles recorded in Google Sheets into platform-specific social posts. Google Gemini summarizes each article, then drafts a detailed LinkedIn post and a short X post. The workflow sends each draft to its platform node, which can publish when configured and run.

## How it works

```text
Google Sheets Trigger (hourly)
             |
             v
    Summarize article (Gemini)
          /             \
         v               v
Draft LinkedIn post    Draft X post
      (Gemini)           (Gemini)
         |                 |
         v                 v
LinkedIn post node      X post node
```

1. **Google Sheets Trigger** polls the configured sheet hourly.
2. **Summarize articles** sends the article field to Gemini for a summary.
3. The workflow branches the summary into two separate drafting chains.
4. **Basic LLM Chain** drafts a professional LinkedIn post.
5. **twitter llm chain** drafts a short post for X.
6. **Create a post** and **Create Tweet** pass the generated text to LinkedIn and X.

## Tech stack

- n8n workflow automation
- Google Sheets Trigger
- Google Gemini through n8n LangChain nodes
- LinkedIn and X nodes

## Files

- `workflow.github.json` — sanitized copy of the supplied workflow for sharing and import.

The workflow file has no saved credential references. The private spreadsheet reference and LinkedIn person identifier were replaced with placeholders. n8n node IDs were regenerated, instance metadata was removed, and the workflow remains inactive. Configure your own spreadsheet and credentials inside n8n after importing.

## Setup

1. Import `workflow.github.json` into your n8n instance.
2. Select your own spreadsheet and tab in the Google Sheets Trigger.
3. Connect Google Sheets and Gemini credentials using n8n's credential manager.
4. Review the article field expression in the summary prompt. The supplied workflow refers to `newskink`; make sure that matches your sheet column or change it.
5. Review the X prompt text; it appears garbled and its 13-word limit may not fit the platform's character limit.
6. If you choose to configure LinkedIn or X, connect your own credentials and verify the destination account and permissions.

## Safety and testing

The LinkedIn and X nodes can publish real posts when configured and run. For a safe demonstration, duplicate the workflow and disconnect or disable both publishing nodes. Test the summary and draft generation using a harmless sample article, then inspect the outputs. Keep the workflow inactive until configuration and destination checks are complete.

The supplied screenshot showed an error on the LinkedIn node and a warning on the X node. This sanitized export has not been imported or tested in another n8n instance. Resolve those node issues and verify the sheet fields, credentials, and prompt expressions before describing it as fully working.

