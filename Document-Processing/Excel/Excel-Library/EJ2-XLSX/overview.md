---
title: EJ2-XLSX Documentation Overview | Syncfusion
description: Complete documentation for EJ2-XLSX - a programmatic XLSX/OOXML class library for JavaScript and TypeScript.
platform: document-processing
control: EJ2-XLSX
documentation: UG
---

# EJ2-XLSX Documentation

EJ2-XLSX is a programmatic XLSX/OOXML class library for JavaScript and TypeScript, enabling you to create, read, edit, and manipulate Excel spreadsheets in web applications and Node.js environments.

## Getting Started

- **[Installation](installation.md)** - Set up EJ2-XLSX in your project
- **[Overview](overview.md)** - Introduction to key features and concepts

## Core Features

### Workbook Management
- **[Workbook](workbook.md)** - Create, open, and manage workbooks
- **[Loading and Saving Workbooks](loading-and-saving-workbooks.md)** - Read and write XLSX files
- **[Worksheets](worksheets.md)** - Work with sheets and tabs

### Data & Formatting
- **[Cell Manipulation](cell-manipulation.md)** - Read and write cell values
- **[Styles & Formatting](styles-and-formatting.md)** - Apply fonts, colors, borders, and fills
- **[Number Formats](number-formats.md)** - Format numbers, dates, and currencies
- **[Rich Text](rich-text.md)** - Create formatted text with multiple styles

### Advanced Features
- **[Data Validation](data-validation.md)** - Set up cell validation rules
- **[Conditional Formatting](conditional-formatting.md)** - Apply conditional formatting rules
- **[Tables](tables.md)** - Create and manage Excel tables
- **[Pivot Tables](pivot-tables.md)** - Create pivot tables and pivot caches
- **[Hyperlinks](hyperlinks.md)** - Add links to cells, web pages, and email addresses
- **[Comments](comments.md)** - Add classic comments and threaded comments
- **[Formulas](formulas.md)** - Work with cell formulas and named ranges

### Security & Protection
- **[Encryption and Decryption](workbook-encryption-and-decryption.md)** - Protect workbooks with passwords
- **[Workbook Protection](workbook-protection.md)** - Lock workbook structure
- **[Sheet Protection](sheet-protection.md)** - Protect sheet cells

### Page Layout & Printing
- **[Page Setup](page-setup.md)** - Configure page orientation, margins, and paper size
- **[Print Settings](print-settings.md)** - Set up print areas and print options
- **[Headers & Footers](headers-and-footers.md)** - Add headers and footers to pages

### Drawing & Visuals
- **[Charts](charts.md)** - Create and customize charts
- **[Images](images.md)** - Insert and position images
- **[Shapes](shapes.md)** - Add shapes and text boxes
- **[Form Controls](form-controls.md)** - Add form controls to sheets

## Platform Support

| Feature | Browser | Node.js |
|---------|---------|---------|
| Create workbooks | ✓ Yes | ✓ Yes |
| Open from bytes | ✓ Yes | ✓ Yes |
| Open from file | ✗ No | ✓ Yes |
| Save to bytes | ✓ Yes | ✓ Yes |
| Save to file | ✗ No | ✓ Yes |
| Encryption/Decryption | ✓ Yes | ✓ Yes |

## Quick Start Examples

### Create and Save a Workbook

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

// Create a new workbook
const workbook = Workbook.create();
const sheet = workbook.sheet(0);

// Add data
sheet.getCell('A1').value = 'Hello';
sheet.getCell('B1').value = 'World';

// Save the workbook
const bytes = await workbook.save();
```

### Open and Read a Workbook

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

// Open an existing workbook
const workbook = await Workbook.open(fileBytes);
const sheet = workbook.sheet(0);

// Read cell values
const value = sheet.getCell('A1').value;
console.log(value); // 'Hello'
```

### Encrypt a Workbook

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const workbook = Workbook.create();
workbook.passwordToOpen = 'MyPassword123';

// Save encrypted
const encryptedBytes = await workbook.save();
```

### Open an Encrypted Workbook

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

// Open and decrypt
const workbook = await Workbook.open(encryptedBytes, 'MyPassword123');
```

## Documentation Structure

### User Guides
Complete how-to documentation for each feature, with examples and best practices.

### API Reference
Formal documentation of public classes, methods, properties, and error types.

### Troubleshooting
Common issues and solutions.

### Interoperability
Notes on compatibility with Microsoft Excel, LibreOffice, and other tools.

## Support & Resources

- **[API Coverage](API-COVERAGE-ENCRYPTION.md)** - Detailed API inventory
- **[Consistency Review](CONSISTENCY-REVIEW.md)** - Documentation quality assurance
- **[Example Verification](EXAMPLE-VERIFICATION.md)** - Code examples testing results

## Key Concepts

### Async/Await Pattern
All file operations in EJ2-XLSX are asynchronous:

```typescript
const workbook = await Workbook.open(fileBytes);
await workbook.save();
```

### Type Safety
Full TypeScript support with strong typing:

```typescript
const workbook: Workbook = Workbook.create();
const sheet: Worksheet = workbook.sheet(0);
const cell: Cell = sheet.getCell('A1');
```

### Error Handling
Typed error classes for proper error handling:

```typescript
import { Workbook, InvalidPasswordError } from '@syncfusion/ej2-xlsx';

try {
  const workbook = await Workbook.open(bytes, 'password');
} catch (error) {
  if (error instanceof InvalidPasswordError) {
    console.log('Wrong password');
  }
}
```

## Browser vs. Node.js

### Browser
- Create and edit workbooks in memory
- Export to bytes for download
- Import from File input or fetch
- No file system access

### Node.js
- All browser capabilities
- Plus: Read/write files from filesystem
- Command-line tools and automation
- Server-side document generation

## Performance & Limitations

- **Speed**: Encrypting/decrypting ~20 MB files takes ~1.1 seconds
- **Memory**: Entire workbook held in memory
- **Randomness**: Uses host CSPRNG (never Math.random)
- **Max file size**: Limited by available memory

## Standards & Specifications

EJ2-XLSX implements:
- **ECMA-376-1** - Office Open XML (OOXML) file format
- **ECMA-376-2** - Office Open XML encryption
- **MS-OFFCRYPTO** - Office Document Cryptography Structure
- **MS-CFB** - Compound File Binary File Format

## License

EJ2-XLSX is licensed under the Syncfusion Community License. See LICENSE file for details.

## Getting Help

- Check the relevant feature documentation
- Review code examples and tutorials
- Consult the FAQ section in specific topics
- Contact Syncfusion support

## Contributing

Found an issue or have a suggestion? Please report it through the appropriate channels.

---

**Last Updated**: 2024  
**Version**: EJ2-XLSX Documentation  
**Status**: Production
