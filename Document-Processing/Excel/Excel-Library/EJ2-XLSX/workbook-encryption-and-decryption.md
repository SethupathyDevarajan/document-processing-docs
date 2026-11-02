---
title: Encryption and Decryption in EJ2-XLSX | Protect Workbooks with Passwords | Syncfusion
description: Learn how to encrypt and decrypt Excel workbooks programmatically using EJ2-XLSX. Protect your spreadsheets with ECMA-376 Agile encryption or open legacy Standard-encrypted files.
platform: document-processing
control: EJ2-XLSX
documentation: UG
---

# Encryption and Decryption

EJ2-XLSX enables you to protect workbooks with password encryption and open encrypted files. The library uses industry-standard ECMA-376 Agile encryption (AES-256-CBC with SHA-512 hashing) for writing encrypted files, and supports reading both Agile and Standard-encrypted workbooks produced by Microsoft Excel 2007 and later.

## Key Features

- **Encrypt on Save**: Apply a password to encrypt the entire workbook during save
- **Decrypt on Open**: Open password-protected files by providing the correct password
- **Industry-Standard Encryption**: Uses ECMA-376 Agile encryption with AES-256-CBC and SHA-512
- **Backward Compatibility**: Opens legacy Standard-encrypted files (Excel 2007 and later)
- **Integrity Protection**: HMAC-SHA512 data-integrity verification
- **Full Workbook Protection**: Encrypts the entire package including all worksheets, styles, and metadata

## Important Distinctions

Workbook encryption (file-level) is separate from workbook structure protection and sheet protection:
- **Workbook Encryption** (`passwordToOpen`): Encrypts the entire file so it cannot be opened without the correct password
- **Workbook Protection** (`workbook.protect()`): Locks the workbook structure (prevents adding/removing/moving sheets) but does not encrypt
- **Sheet Protection**: Protects individual sheet cells from editing while allowing navigation

These features can be combined independently on the same workbook.

## Setting a Password to Encrypt a Workbook

### Basic Encryption

Use the `passwordToOpen` property to set a password. The workbook will be encrypted when saved:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const workbook = Workbook.create();
const sheet = workbook.sheet(0);
sheet.getCell('A1').value = 'Confidential Data';

// Set the open password
workbook.passwordToOpen = 'MySecurePassword123';

// Save the encrypted workbook
const bytes = await workbook.save();
```

### Password Validation

When you set a password, the library validates that:
- The password is between 1 and 255 characters (Excel limit)
- The password is a valid string
- An invalid password throws `InvalidPasswordError`

```typescript
const workbook = Workbook.create();

try {
  // This will throw InvalidPasswordError
  workbook.passwordToOpen = 'x'.repeat(256);
} catch (error) {
  console.log(error.code); // 'INVALID_PASSWORD'
  console.log(error.message);
}

// Valid password (exactly 255 characters)
workbook.passwordToOpen = 'x'.repeat(255); // OK
```

### Clearing a Password

Set the password to `undefined`, `null`, or an empty string to remove encryption:

```typescript
const workbook = Workbook.create();
workbook.passwordToOpen = 'secret';
console.log(workbook.passwordToOpen); // 'secret'

// Remove encryption
workbook.passwordToOpen = undefined;
console.log(workbook.passwordToOpen); // undefined

// The workbook will now save as plain (unencrypted) XLSX
const bytes = await workbook.save();
```

## Opening Encrypted Workbooks

### Opening from Bytes

Use the `Workbook.open()` static method with a password to decrypt and open an encrypted file:

```typescript
import { Workbook, InvalidPasswordError } from '@syncfusion/ej2-xlsx';

const encryptedBytes = /* ... */; // Your encrypted file bytes

try {
  const workbook = await Workbook.open(encryptedBytes, 'MySecurePassword123');
  const data = workbook.sheet(0).getCell('A1').value;
  console.log(data); // 'Confidential Data'
} catch (error) {
  if (error instanceof InvalidPasswordError) {
    console.log('Password is missing or incorrect');
  }
}
```

### Opening from File Path (Node.js)

In Node.js environments, you can open directly from a file path:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const workbook = await Workbook.open('./encrypted-file.xlsx', 'password123');
const value = workbook.sheet(0).getCell('A1').value;
```

### Opening from ArrayBuffer

The `open` method accepts both `Uint8Array` and `ArrayBuffer`:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const buffer = /* ... */; // ArrayBuffer from File input or fetch
const workbook = await Workbook.open(buffer, 'password123');
```

### Handling a Non-Encrypted File

If you call `open()` with a password on a non-encrypted file, the password is silently ignored and the file opens normally:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const plainBytes = await Workbook.create().save();

// Password is ignored for plain files
const workbook = await Workbook.open(plainBytes, 'ignored-password');
console.log(workbook.passwordToOpen); // undefined
```

## Re-Encrypting Modified Workbooks

When you open an encrypted workbook and make changes, the password is preserved:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

// Open an encrypted file
const encrypted = /* ... encrypted bytes ... */;
const workbook = await Workbook.open(encrypted, 'oldPassword');

console.log(workbook.passwordToOpen); // 'oldPassword'

// Make changes
workbook.sheet(0).getCell('B1').value = 'Updated Data';

// Save re-encrypts with the same password (using a fresh salt and key)
const reencrypted = await workbook.save();

// The file can still be opened with the old password
const reopened = await Workbook.open(reencrypted, 'oldPassword');
```

## Changing the Password

To change the password, open the encrypted file and assign a new password:

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

const encrypted = /* ... encrypted bytes ... */;
const workbook = await Workbook.open(encrypted, 'oldPassword');

// Change the password
workbook.passwordToOpen = 'newPassword456';

// Save with the new password
const bytes = await workbook.save();

// Old password no longer works
try {
  await Workbook.open(bytes, 'oldPassword'); // Throws InvalidPasswordError
} catch (error) {
  console.log('Old password rejected');
}

// New password works
const reopened = await Workbook.open(bytes, 'newPassword456');
```

## Decrypting a Workbook (Removing Encryption)

To save an encrypted workbook as plain (unencrypted):

```typescript
import { Workbook } from '@syncfusion/ej2-xlsx';

// Open encrypted file
const encrypted = /* ... encrypted bytes ... */;
const workbook = await Workbook.open(encrypted, 'password123');

console.log(workbook.passwordToOpen); // 'password123'

// Remove the password
workbook.passwordToOpen = undefined; // or null or ''

// Save as plain XLSX (no encryption)
const plainBytes = await workbook.save();

// Verify it's no longer encrypted
const reopened = await Workbook.open(plainBytes);
console.log(reopened.passwordToOpen); // undefined
```

## Supported Encryption Schemes

### Writing: ECMA-376 Agile (Always)

When you set `passwordToOpen` and save, EJ2-XLSX always writes using modern ECMA-376 Agile encryption:

- **Algorithm**: AES-256-CBC (256-bit key)
- **Hash Function**: SHA-512
- **Iterations**: 100,000 password hashing rounds
- **Block Size**: 4,096 bytes
- **Integrity**: HMAC-SHA512 over the entire encrypted package
- **Fresh Salt & Key**: Generated on each save for maximum security

### Reading: Multiple Schemes

EJ2-XLSX can read files encrypted with:

#### Agile Encryption (Modern, Recommended)
- Supports any hash algorithm: SHA-1, SHA-256, SHA-384, SHA-512
- Supports AES key sizes: 128-bit, 192-bit, 256-bit
- Spin count: any value up to 10,000,000

#### Standard Encryption (Legacy, Excel 2007–2019)
- Algorithm: AES-128/192/256-ECB
- Hash: SHA-1
- Iterations: 50,000 password hashing rounds
- Produced by Microsoft Excel 2007 through Excel 2019

## Error Handling

### InvalidPasswordError

Thrown when:
- The password is missing or incorrect when opening an encrypted file
- The password is too long (>255 characters) when setting `passwordToOpen`
- The password is empty (0 characters) when setting `passwordToOpen`

```typescript
import { Workbook, InvalidPasswordError } from '@syncfusion/ej2-xlsx';

try {
  const workbook = await Workbook.open(encryptedBytes, 'wrongPassword');
} catch (error) {
  if (error instanceof InvalidPasswordError) {
    console.log('Error code:', error.code); // 'INVALID_PASSWORD'
    console.log('Details:', error.message);
  }
}

try {
  workbook.passwordToOpen = 'x'.repeat(256);
} catch (error) {
  if (error instanceof InvalidPasswordError) {
    console.log('Password too long');
  }
}
```

### UnsupportedEncryptionError

Thrown when the file uses an encryption scheme this library cannot read:

```typescript
import { Workbook, UnsupportedEncryptionError } from '@syncfusion/ej2-xlsx';

try {
  // File with legacy .xls format or unsupported RMS/certificate encryption
  const workbook = await Workbook.open(legacyBytes, 'password');
} catch (error) {
  if (error instanceof UnsupportedEncryptionError) {
    console.log('Error code:', error.code); // 'UNSUPPORTED_ENCRYPTION'
    console.log('This encryption scheme is not supported');
  }
}
```

## Complete Example

Here is a complete example combining encryption, modification, and decryption:

```typescript
import { Workbook, InvalidPasswordError } from '@syncfusion/ej2-xlsx';
import { readFileSync, writeFileSync } from 'fs';

async function demonstrateEncryption() {
  // Create a new workbook
  const workbook = Workbook.create();
  const sheet = workbook.sheet(0);
  
  // Add some data
  sheet.getCell('A1').value = 'Employee ID';
  sheet.getCell('B1').value = 'Salary';
  sheet.getCell('A2').value = 'E001';
  sheet.getCell('B2').value = 75000;
  sheet.getCell('A3').value = 'E002';
  sheet.getCell('B3').value = 85000;
  
  // Encrypt the workbook
  workbook.passwordToOpen = 'CompanySecret2024';
  
  // Save encrypted
  const encryptedBytes = await workbook.save();
  writeFileSync('sensitive-data.xlsx', encryptedBytes);
  console.log('✓ Workbook encrypted and saved');
  
  // --- Later: Open and modify ---
  const encrypted = readFileSync('sensitive-data.xlsx');
  
  try {
    const opened = await Workbook.open(encrypted, 'CompanySecret2024');
    console.log('✓ Workbook decrypted successfully');
    
    // Modify data
    opened.sheet(0).getCell('B2').value = 78000;
    
    // Re-encrypt with same password
    const modified = await opened.save();
    writeFileSync('sensitive-data.xlsx', modified);
    console.log('✓ Modifications saved (re-encrypted)');
    
    // Change password for next time
    opened.passwordToOpen = 'NewSecret2025';
    const newEncrypted = await opened.save();
    writeFileSync('sensitive-data.xlsx', newEncrypted);
    console.log('✓ Password changed');
    
  } catch (error) {
    if (error instanceof InvalidPasswordError) {
      console.error('✗ Wrong password or missing password');
    } else {
      throw error;
    }
  }
}

demonstrateEncryption();
```

## Performance Considerations

- **Encryption Speed**: A 20 MB workbook typically encrypts in ~1.1 seconds
- **Decryption Speed**: A 20 MB workbook typically decrypts in ~1.1 seconds
- **Memory**: Entire workbook is held in memory during encryption/decryption
- **Salt & Key Generation**: Uses the host's cryptographic random source (never `Math.random`)

## Security Notes

1. **Password Strength**: Use strong, unique passwords. Encourage users to use 12+ characters with mixed case and symbols.
2. **Transport**: Send encrypted files over secure channels (HTTPS, VPN, etc.).
3. **Storage**: Consider how the password is communicated to recipients—never hardcode passwords in source code.
4. **Data Integrity**: The HMAC-SHA512 integrity check detects file corruption, but not intentional tampering.
5. **Randomness**: Fresh salts and initialization vectors are generated for each save using the host CSPRNG.

## Related Topics

- [Workbook Protection](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/workbook-protection) — Lock workbook structure
- [Sheet Protection](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/sheet-protection) — Protect individual sheets
- [Loading and Saving Workbooks](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/loading-and-saving-workbooks) — Working with workbook files

## API Reference

### Workbook Class

#### Properties

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `passwordToOpen` | `string \| undefined` | Get/Set | Gets or sets the open password for file-level encryption. Setting a non-empty password encrypts on save; `undefined`/`null`/`''` removes encryption. |

#### Static Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `open()` | `static async open(data: Uint8Array \| ArrayBuffer, password?: string): Promise<Workbook>` | Opens an Excel workbook from bytes, decrypting if encrypted. If the file is encrypted and no password is provided, throws `InvalidPasswordError`. |
| `open()` | `static async open(filePath: string, password?: string): Promise<Workbook>` | Opens an Excel workbook from a file path (Node.js only), decrypting if encrypted. |

#### Instance Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `save()` | `async save(): Promise<Uint8Array>` | Saves the workbook to bytes. If `passwordToOpen` is set, the bytes are an encrypted file. |
| `save()` | `async save(filePath: string): Promise<void>` | Saves the workbook to a file path (Node.js only). If `passwordToOpen` is set, the file is encrypted. |

### Error Classes

#### InvalidPasswordError

**Code**: `INVALID_PASSWORD`

Thrown when:
- Opening an encrypted file without a password or with an incorrect password
- Setting `passwordToOpen` to a password longer than 255 characters
- Setting `passwordToOpen` to an empty string (0 characters)

```typescript
import { InvalidPasswordError } from '@syncfusion/ej2-xlsx';

try {
  // ...
} catch (error) {
  if (error instanceof InvalidPasswordError) {
    console.log(error.code); // 'INVALID_PASSWORD'
  }
}
```

#### UnsupportedEncryptionError

**Code**: `UNSUPPORTED_ENCRYPTION`

Thrown when attempting to open a file with an unsupported encryption scheme, such as:
- Legacy .xls Compound File Binary (CFB) format
- Extensible encryption (certificate-based or RMS)

```typescript
import { UnsupportedEncryptionError } from '@syncfusion/ej2-xlsx';

try {
  // ...
} catch (error) {
  if (error instanceof UnsupportedEncryptionError) {
    console.log(error.code); // 'UNSUPPORTED_ENCRYPTION'
  }
}
```

## Browser vs. Node.js

| Feature | Browser | Node.js |
|---------|---------|---------|
| Encrypt/Decrypt | ✓ Yes | ✓ Yes |
| `open(bytes, password)` | ✓ Yes | ✓ Yes |
| `open(filePath, password)` | ✗ No | ✓ Yes |
| `save()` (to bytes) | ✓ Yes | ✓ Yes |
| `save(filePath)` | ✗ No | ✓ Yes |

## Frequently Asked Questions

### Q: Can I encrypt a workbook without opening it first?

**A:** Yes. Create a new workbook or load an unencrypted one, set `passwordToOpen`, and save:

```typescript
const workbook = Workbook.create();
workbook.passwordToOpen = 'password123';
const encryptedBytes = await workbook.save();
```

### Q: What happens if I forget the password?

**A:** There is no password recovery or bypass. Store passwords securely and communicate them through separate secure channels.

### Q: Can I use the same password for both encryption and sheet protection?

**A:** Yes, they are independent features and can use the same password. They protect different aspects:
- `passwordToOpen`: File-level encryption (no access without password)
- `sheet.protect()`: Cell editing (sheet is visible but cells are locked)

### Q: Are special characters supported in passwords?

**A:** Yes. Passwords support the full Unicode character set. Internally they are encoded as UTF-16LE (Excel standard).

### Q: Can I encrypt only specific sheets?

**A:** No. File-level encryption encrypts the entire workbook. If you need sheet-level privacy, use sheet protection instead.

### Q: How does EJ2-XLSX compare to the .NET Excel library?

**A:** The EJ2-XLSX API mirrors the .NET XlsIO library:
- `workbook.passwordToOpen` ↔ `IWorkbook.PasswordToOpen`
- `Workbook.open(data, password)` ↔ `IWorkbooks.Open(stream, ..., password)`

EJ2-XLSX supports reading legacy Standard-encrypted files but writes only Agile encryption (more secure).

## Standards and Specifications

- **ECMA-376-2**: Office Open XML File Formats (encryption outside ZIP package)
- **MS-OFFCRYPTO**: Office Document Cryptography Structure
- **MS-CFB**: Compound File Binary File Format
- **NIST SP 800-38A**: Recommendation for Block Cipher Modes of Operation (CBC)

## See Also

- [Workbook](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/workbook)
- [Worksheet](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/worksheet)
- [Workbook Protection](https://help.syncfusion.com/document-processing/excel/ej2-xlsx/workbook-protection)
