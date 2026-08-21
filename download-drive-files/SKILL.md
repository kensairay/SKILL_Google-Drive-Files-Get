---
name: download-drive-files
description: Download files from Google Drive links through the Google Drive connector instead of browser page access. Use when the user provides a Google Drive file or folder URL, asks to download Drive files, says browser access is blocked, or wants connector/API-based downloading into the local workspace.
---

# Download Drive Files

## Overview

Use connector-first Google Drive downloading for local file retrieval. This is especially useful when direct browser access to `drive.google.com` is blocked by network filtering but the connected Drive account is authorized to read the files.

## Workflow

1. Confirm the user provided a Google Drive file or folder URL.
2. If Google Drive tools are not visible, use tool discovery for Google Drive folder listing, metadata, and raw file fetch tools.
3. For a folder URL, list the folder contents first and capture each item name, ID, MIME type, size, and URL.
4. For a single file URL, read metadata first when possible so the MIME type and expected size are known.
5. Download files with the Drive connector:
   - Use raw file download for PDFs, images, ZIP files, Office files, CSVs, audio, video, and other non-native Drive files.
   - Use an appropriate export format for native Google Docs, Sheets, or Slides when the user asks for local files. Default to DOCX, XLSX, and PPTX respectively unless the user asks for PDF or another format.
6. Save downloads under the current workspace in `downloaded_drive_files` unless the user names a different destination.
7. Preserve Drive filenames. If a filename already exists, avoid overwriting by adding a short suffix.
8. Verify the result by listing local filenames and byte sizes. Compare sizes to Drive metadata when size is available.
9. Report the saved paths, filenames, sizes, and any files skipped or inaccessible.

## Failure Handling

- If the connector can list the folder but a browser or CLI downloader cannot, continue with the connector path and mention that browser access may be blocked separately from API access.
- If the connector cannot access the file or folder, explain that Drive sharing or account authorization is required.
- If the Drive folder is empty through the connector, report that no downloadable items were visible to the connected account.
- Do not treat temporary connector download URLs as durable. Use them only to complete the current local save.
- Do not imply that this bypasses company policy. State that the download still depends on authorized Drive access and should follow the user's organization rules.
