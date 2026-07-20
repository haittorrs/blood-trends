# Blood Trends

Blood Trends is a private, on-device blood test tracker designed to help users store, review, and compare blood test results over time.

The app runs entirely in the browser as a Progressive Web App (PWA). Users can upload a blood test PDF, review the detected values, save the results locally, and view trends for supported blood markers.

> **Important:** Blood Trends is a personal record-keeping tool. It is not a medical device and does not provide medical advice. Laboratory reference ranges shown on official reports always take priority over the built-in guide ranges.

## Features

- Create a PIN-protected local account
- Encrypt stored data using AES-256-GCM
- Derive the encryption key from the PIN using PBKDF2-SHA256
- Upload text-based blood test PDF files
- Automatically detect supported blood markers and values
- Review and correct extracted values before saving
- Add missing or custom markers manually
- View previous results for each marker
- Display simple trend charts
- Show rising, falling, or steady trends
- Flag values outside the built-in guide ranges
- Export records as a JSON backup
- Import and merge a previous backup
- Change the PIN
- Delete individual reports or erase all local data
- Install the app on a phone or computer as a PWA
- Open the app offline after the required files have been cached

## Privacy and security

Blood Trends is designed so that personal data remains on the user's device.

- Blood test PDFs are processed in the browser.
- Saved records are encrypted before being written to browser storage.
- Records are stored in `localStorage` for the app's website origin.
- The PIN itself is not stored.
- There is no account system, database, analytics service, or application server.
- The only external code loaded by the app is PDF.js from cdnjs for reading PDF files.
- Exported JSON backups are **not encrypted** and should be stored securely.

The app automatically locks after it has been left in the background for more than three minutes.

There is no PIN recovery system. Losing the PIN means the encrypted local data cannot be unlocked. Keep regular exported backups.

## Supported markers

The app includes built-in support for common blood markers, including:

- HbA1c
- Fasting glucose
- Total cholesterol
- HDL cholesterol
- LDL cholesterol
- Non-HDL cholesterol
- Cholesterol to HDL ratio
- Triglycerides
- Vitamin D
- Vitamin B12
- Folate
- Ferritin
- TSH
- ALT
- AST
- Gamma GT
- ALP
- Bilirubin
- Albumin
- Creatinine
- eGFR
- Urea
- Sodium
- Potassium
- CRP
- Haemoglobin
- White cell count
- Platelets

Custom markers can also be added manually.

## Project structure

```text
blood-trends/
├── index.html
├── manifest.json
├── sw.js
├── icon-192.png
├── icon-512.png
├── apple-touch-icon.png
├── sample-report.pdf
└── README.md
```

### File overview

| File | Purpose |
|---|---|
| `index.html` | Contains the user interface, encryption, PDF parsing, storage, charts, and all app logic |
| `manifest.json` | Defines the Progressive Web App name, colours, icons, and start page |
| `sw.js` | Service worker used to cache the app shell and support offline use |
| `icon-192.png` | 192 × 192 PWA icon |
| `icon-512.png` | 512 × 512 PWA icon |
| `apple-touch-icon.png` | Icon used when installing the app on an Apple device |
| `sample-report.pdf` | Synthetic blood test report for safe testing |

## Running the app locally

The project must be opened through a local web server. Do not test it by double-clicking `index.html`, because a `file://` page may not provide the secure browser context required by the Web Crypto API.

### Option 1: VS Code Live Server

1. Open the project folder in Visual Studio Code.
2. Install the **Live Server** extension.
3. Right-click `index.html`.
4. Select **Open with Live Server**.
5. Open the displayed local address, such as:

```text
http://127.0.0.1:5500/
```

### Option 2: Python local server

Open a terminal inside the project folder and run:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

`localhost` is treated as a secure context by modern browsers, allowing the encryption system to work during local development.

## Testing the app

A synthetic file named `sample-report.pdf` is included for testing.

1. Start the app through a local server.
2. Create a PIN containing at least six digits.
3. Select **Add a blood test report (PDF)**.
4. Upload `sample-report.pdf`.
5. Review the detected date and marker values.
6. Correct or remove any incorrect rows.
7. Save the report.
8. Open a marker card to view its history and chart.
9. Delete the test report when finished.

The sample report contains no real patient data.

## Deployment with GitHub Pages

1. Create a GitHub repository.
2. Upload all required project files.
3. Open the repository's **Settings**.
4. Select **Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select the `main` branch and the `/ (root)` folder.
7. Save the settings.
8. Wait for GitHub Pages to publish the site.

The deployed address will normally follow this format:

```text
https://YOUR-USERNAME.github.io/REPOSITORY-NAME/
```

GitHub Pages provides HTTPS, which is required for browser encryption and service workers outside `localhost`.

## Installing as an app

### iPhone or iPad

1. Open the deployed website in Safari.
2. Tap the Share button.
3. Select **Add to Home Screen**.
4. Tap **Add**.

### Desktop browser

In a supported browser, open the deployed site and use the browser's **Install app** option.

## PDF compatibility

Blood Trends works best with text-based PDF reports where the marker name, value, unit, and reference range are readable as text.

Scanned image-only PDFs may not be parsed automatically because the current version does not include OCR. Values from those reports can still be entered manually through the review screen.

Users should always compare detected values with the original laboratory report before saving.

## Backups

Use **Settings → Export my data** after adding or changing records.

The export creates a readable JSON file containing the stored results. This file is not encrypted, so it should be kept in a protected folder or secure cloud storage location.

To restore data:

1. Open **Settings**.
2. Select **Import a backup**.
3. Choose a previous Blood Trends JSON export.
4. The app will merge values that are not already stored for the same date and marker.

## Resetting the app

To erase data normally, use:

```text
Settings → Erase everything
```

If the PIN has been forgotten, remove the website's stored data through the browser settings, then reopen the app and create a new PIN. Previously exported backups can then be imported.

## Limitations

- Built-in reference ranges are general guide values only.
- Laboratory ranges may vary.
- PDF extraction may misread unusual report layouts.
- Scanned PDFs are not automatically recognised.
- Data is tied to the browser and website origin unless exported.
- Clearing browser storage deletes the locally stored encrypted records.
- Forgotten PINs cannot be recovered.

## Technology

- HTML
- CSS
- Vanilla JavaScript
- Web Crypto API
- AES-256-GCM
- PBKDF2-SHA256
- PDF.js
- Service Workers
- Web App Manifest
- Local browser storage

## Development note

This project was created with assistance from artificial intelligence. The generated code was reviewed, tested, and adjusted during development.

## Licence

No licence has currently been specified.

Without a licence, the repository remains protected by default copyright law. Add a `LICENSE` file before allowing other people to copy, modify, or redistribute the project.

## Disclaimer

Blood Trends is intended only for personal record keeping and trend visualisation.

It does not diagnose conditions, interpret results medically, recommend treatments, or replace professional medical advice. Always consult a qualified healthcare professional about blood test results or health concerns.
