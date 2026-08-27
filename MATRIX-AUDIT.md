# Matrix Audit

## Failing Combinations

### 1. OS: windows-latest, Node: 18
- **Step Name:** npm test
- **Exact Error Line:** `Expected: "line one\nline two\nline three\n", Received: "line one\r\nline two\r\nline three\r\n"` and `Expected: "C:\\...\\output\\report.txt", Received: "C:\.../output/report.txt"` (path mismatch)
- **Classification:** OS-specific
- **Planned Fix:** Use `path.join` for path concatenation in `src/fileUtils.js`. Normalize line endings (e.g., using `.replace(/\r\n/g, '\n')`) in `src/fileUtils.test.js` before making the assertion.

### 2. OS: windows-latest, Node: 20
- **Step Name:** npm test
- **Exact Error Line:** `Expected: "line one\nline two\nline three\n", Received: "line one\r\nline two\r\nline three\r\n"` and `Expected: "C:\\...\\output\\report.txt", Received: "C:\.../output/report.txt"` (path mismatch)
- **Classification:** OS-specific
- **Planned Fix:** Same as above. Use `path.join` for path concatenation and normalize line endings in test assertions.

### 3. OS: ubuntu-latest, Node: 22
- **Step Name:** npm test
- **Exact Error Line:** `TypeError: crypto.createCipher is not a function`
- **Classification:** runtime version
- **Planned Fix:** Replace deprecated `crypto.createCipher` and `crypto.createDecipher` with `crypto.createCipheriv` and `crypto.createDecipheriv` in `src/cryptoUtils.js` since they were removed in Node 22.

### 4. OS: windows-latest, Node: 22
- **Step Name:** npm test
- **Exact Error Line:** `TypeError: crypto.createCipher is not a function` (and the OS-specific path/line-ending errors).
- **Classification:** runtime version and OS-specific
- **Planned Fix:** Apply both the cross-platform path/line-ending fixes and the `crypto.createCipheriv` update.
