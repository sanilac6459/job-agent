# Phil — Job Applier Agent

Phil is an AI-powered job application automation agent that parses your resume, finds relevant application fields on job postings, and generates and fills in answers automatically — with tracing, evaluation, and retry logic built in.

## Demo
 
[Click here!](https://drive.google.com/file/d/1NNQAlaI6GqRZ3moRA5YVlMKBbLKKBzz-/view?pli=1)


## Features

- **Resume parsing & caching** — parses a resume once and caches the result, keyed by a hashed email, so repeat runs skip redundant parsing.
- **Vector storage** — resume and profile data stored in **ChromaDB (cloud)** for fast retrieval during application generation.
- **Multi-agent browser automation** — uses `browser_use` to navigate job application pages and fill out multi-agent browser flows.
- **Short-answer generation** — uses **Gemini** (via **OpenRouter**) through **LangChain** to generate short-answer responses tailored to each application field.
- **Field evaluation metrics** — scores generated answers against each field's requirements.
- **Feedback retry loop** — automatically retries and refines answers that don't meet evaluation thresholds.
- **CSV logging** — logs every application submission and outcome to CSV for tracking.
- **LangSmith tracing** — `@traceable` decorators throughout the pipeline for full run tracing and debugging.

## Tech Stack

| Tool | Role |
|---|---|
| **LLM — Gemini 2.5 Flash-Lite** | Parses the resume, generates short-answer responses, and fills in application fields |
| **browser_use** | Lets the agent interact with the browser |
| **ChromaDB** | Stores the user's resume and additional info for retrieval |
| **LangSmith** | Traces each function call |
| **OpenRouter** | Defines/routes the LLM model used |

## How It Works

1. **Parse resume** — extract structured data from the user's resume and cache it by hashed email.
2. **Store in ChromaDB** — embed and store resume/profile data for retrieval.
3. **Navigate application** — a multi-agent browser automation flow opens and walks through the job application form.
4. **Generate answers** — short-answer responses are generated per field using the LLM and stored resume context.
5. **Evaluate** — each generated answer is scored against field requirements.
6. **Retry if needed** — a feedback loop regenerates answers that fail evaluation.
7. **Log results** — every attempt is logged to CSV, with full traces available in LangSmith.

