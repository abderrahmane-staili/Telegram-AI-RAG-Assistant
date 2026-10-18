# Telegram AI RAG Assistant

An n8n workflow for answering Telegram questions with information retrieved from a private document collection. The project combines document ingestion from Google Drive, PostgreSQL/PGVector semantic search, and OpenAI-powered text, voice, and image handling.

> **Workflow preview:** Open [`index.html`](./index.html) to view the interactive, read-only workflow diagram. The diagram is also available as [`workflow-design.html`](./rag%20version%202/workflow-design.html). It is a standalone HTML page and does not expose workflow controls or require external assets.

## What it does

The n8n workflow has two connected use cases:

1. **Build the knowledge base:** a Google Drive trigger starts the ingestion flow. The file is downloaded, its content is extracted, and the resulting document and embeddings are sent to a PostgreSQL PGVector store.
2. **Answer Telegram messages:** an incoming Telegram message is routed by type. Text is prepared for the AI Agent; voice messages are downloaded and processed; image messages are analyzed. The AI Agent can search the PGVector store and sends its response back to Telegram.

The agent's instructions tell it to ground answers in retrieved documents and to say when it cannot find relevant information. As with any LLM workflow, test the responses against your own data before relying on them.

## Architecture

```text
Knowledge ingestion
Google Drive Trigger -> Download file -> Extract file -> PostgreSQL PGVector Store
                                                     ^               ^
                                                     | document      | embeddings
                                               Document loader   OpenAI embeddings

Telegram question
Telegram Trigger -> Route message
                    ├─ Text -> Prepare fields ---------------------┐
                    ├─ Voice -> Download -> Transcribe ------------┤
                    └─ Image -> Download/analyze ------------------┤
                                                                    v
                                                         AI Agent + memory
                                                           |          ^
                                                           |          |
                                                     Telegram reply  PGVector search
```

The exported workflow contains 20 executable nodes and 5 canvas notes. The preview presents the node names, node types, and connections as a read-only map.

## Project files

| Path | Description |
| --- | --- |
| [`index.html`](./index.html) | Entry page that opens the workflow diagram directly. |
| [`rag version 2/workflow-design.html`](./rag%20version%202/workflow-design.html) | Standalone visual workflow diagram. |
| [`rag version 2/workflow.json`](./rag%20version%202/workflow.json) | n8n workflow export; import this into your n8n instance. |
| [`rag version 2/image.png`](./rag%20version%202/image.png) | Image file included in the original repository. |
| [`rag1.json`](./rag1.json) | Earlier workflow export included in the original repository. |

## Requirements

- An n8n instance with the Telegram, Google Drive, OpenAI, and PostgreSQL/PGVector integrations available.
- A Telegram bot and a Telegram credential configured in n8n.
- Google Drive OAuth credentials with access to the documents to ingest.
- An OpenAI API credential for the language model, embeddings, and media-processing nodes used by the workflow.
- A PostgreSQL database configured for the PGVector integration. Configure the target table/collection and embedding settings to match your own database.

The JSON export contains workflow configuration and credential references, **not working API keys**. Credentials and provider resources must be configured in your own n8n instance.

## Import and configure

1. Download [`workflow.json`](./rag%20version%202/workflow.json) from this repository.
2. In n8n, import the JSON using **Workflows → Import from File** (the exact menu wording can vary by n8n version).
3. Open the imported workflow and assign your own Telegram, Google Drive, OpenAI, and PostgreSQL credentials to the relevant nodes.
4. Review the Google Drive trigger, document extraction, PGVector table/collection, embedding model, and Telegram routing settings. Update them for your account and data.
5. Test document ingestion first, then test text, voice, and image messages with your Telegram bot.
6. Verify that answers are grounded in your documents and that the bot responds appropriately when the knowledge base has no relevant information.
7. Activate the workflow only after the tests succeed.

Do not commit API keys, bot tokens, private documents, or other secrets to the repository.

## View the diagram

- **Locally:** open [`index.html`](./index.html) in a browser. It redirects to the standalone diagram inside `rag version 2`.
- **On GitHub Pages:** enable Pages for the repository and deploy from the `main` branch, repository root. Once the deployment completes, the root site URL will open the diagram through `index.html` (for example, `https://abderrahmane-staili.github.io/Telegram-AI-RAG-Assistant/`).
- **Source file:** [`workflow-design.html`](./rag%20version%202/workflow-design.html).

GitHub Pages is not enabled by this project fileset itself; it must be configured in the repository's **Settings → Pages** after the files are pushed.

## Original n8n workflow

The workflow was provided through this n8n URL: [Open the workflow](https://n8ninstance.bmo-n8n.buzz/workflow/FXPEvIjgJU1RohZJ). Access may require permission to the n8n instance.

## License

No license file was present in the original repository. Unless the repository owner adds a license, reuse and redistribution are not granted by this README.
