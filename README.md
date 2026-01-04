# Python File Search Engine

A fast and flexible command-line tool to search for files across directories and subdirectories with keyword matching, extension filtering, and case-sensitive options.

## Features

- **Recursive Search**: Automatically searches through all subdirectories
- **Keyword Matching**: Find files by keyword in their filenames
- **Extension Filtering**: Filter results by one or multiple file extensions
- **Case-Sensitive Option**: Choose between case-insensitive (default) or case-sensitive search
- **File Information**: Display file paths and sizes in the results
- **Error Handling**: Validates input and handles missing directories gracefully
- **Easy to Use**: Simple command-line interface with helpful usage instructions

## Requirements

- Python 3.6 or higher
- No external dependencies (uses built-in `pathlib` and `sys` modules)

## Installation

1. Clone or download the project:
```bash
git clone https://github.com/yourusername/python-file-search-engine.git
cd python-file-search-engine
```

2. No additional packages to install - the script uses only Python standard library

## Usage

### Basic Syntax

```bash
python script.py <directory> <keyword> [options]
```

### Arguments

- `<directory>`: Path to the root directory to search (use `.` for current directory)
- `<keyword>`: The keyword to search for in filenames

### Options

| Option | Short Form | Description |
|--------|-----------|-------------|
| `--ext <ext1,ext2,...>` | `-e` | Filter by file extensions (comma-separated) |
| `--case-sensitive` | `-c` | Perform case-sensitive search |

## Examples

### Example 1: Search for all files containing "report"

```bash
python script.py . report
```

**Output:**
```
Searching in '.' and subdirectories...

======================================================================
SEARCH RESULTS
======================================================================
Keyword: 'report' (case-insensitive)
Matches found: 3
======================================================================

  1. ./documents/annual_report.pdf
     Size: 2.45 MB

  2. ./documents/2024_report.docx
     Size: 156,234 bytes

  3. ./archive/old_reports/q1_report.txt
     Size: 45,678 bytes

======================================================================
```

### Example 2: Search for PDF and DOCX files containing "invoice"

```bash
python script.py ./documents invoice -e pdf,docx
```

**Output:**
```
Searching in './documents' and subdirectories...

======================================================================
SEARCH RESULTS
======================================================================
Keyword: 'invoice' (case-insensitive)
Extensions: pdf, docx
Matches found: 2
======================================================================

  1. ./documents/2024_invoice.pdf
     Size: 512,456 bytes

  2. ./documents/January/invoice_receipt.docx
     Size: 89,234 bytes

======================================================================
```

### Example 3: Case-sensitive search for "Config" in log files

```bash
python script.py /var/logs Config -c -e log,txt
```

This will only match filenames with "Config" (exact capitalization) in `.log` and `.txt` files.

### Example 4: Search entire home directory for "backup"

```bash
python script.py ~ backup -e zip,tar,gz
```

This searches your home directory for backup archives in compressed formats.

## How It Works

1. **Path Validation**: The script verifies that the specified directory exists and is accessible
2. **Recursive Traversal**: Uses `pathlib.Path.rglob()` to recursively search all subdirectories
3. **Filtering**: Applies extension and case-sensitivity filters during the search
4. **Results**: Returns matching files with their full paths and file sizes
5. **Display**: Formats and displays results in a clean, organized manner

## Tips & Best Practices

- Use `.` to search the current directory
- Use `~` to search your home directory
- Use `/` to search from the root (Linux/Mac only)
- Extension names are case-insensitive; use `pdf` or `PDF` interchangeably
- For multiple extensions, separate them with commas and no spaces: `-e pdf,docx,xlsx`
- Use `--case-sensitive` when searching for specific naming patterns or proper nouns
- On large directories with many files, the initial search may take a few seconds

## Troubleshooting

### Error: "Directory does not exist"
Check that the path is correct and the directory exists:
```bash
# Fix: Use correct path
python script.py /correct/path keyword
```

### No results found
The keyword might not match any filenames, or the extension filter is too restrictive:
```bash
# Try without extension filter
python script.py . keyword

# Try case-sensitive search
python script.py . keyword -c
```

### Permission denied
You may not have read access to certain directories. Try with a directory you have permissions for or use `sudo` (use with caution).

## Performance Notes

- Searching large directory trees with millions of files may take time
- Results are sorted alphabetically before display
- File size information requires reading file metadata (minimal performance impact)

## License

MIT License - Feel free to use and modify for your projects

## Contributing

Contributions are welcome! Feel free to fork the project and submit pull requests for improvements.

## Author

Created as a practical Python utility for efficient file searching across directories.
