# File Structure 
# Doc File 📄

## Structure

- **Information Block:** Contains metadata about the document.
- **Mainstream:** The primary content stream.
- **Table Stream:** Contains table data.
- **Summary:** A brief overview of the document.

## Analysis Checklist

- [ ]  **Check Header:** Verify the document header for consistency.
- [ ]  **Check Trailer:** Contains `docpropd` which holds metadata.
- [ ]  **MicroScript:** Embedded scripts within the document.
- [ ]  **File Version:** Check the version of the document.
- [ ]  **Any Known Vulnerabilities:** Look for any known security issues.

---

# JPEG FF D8 🖼

Usually used by cameras.

## Extension

- **jpg**
- **jpe**
- **jfif**

## Structure

- **Header:** Contains file information.
- **Metadata:** Stores information about the image.
- **Footer:** Marks the end of the file.

---

# PDF 📃

The most used file type.

## Structure

- **Header:** Identifies the file as a PDF.
- **Body (obj - endobj):** Contains the document content.
- **Xref Table:** Maps the objects in the body.
- **Trailer:** Contains information about the document.

### Body

It contains `obj` and `endobj`.

More than one object referring to the same entry are called `stream` and `endstream`.

### Xref

- The first line `1 7` (1 = count start from 1, 7 = number of the entries).
- **10 bytes for the offset**.
- **5 bytes for object generation number**.
- `f` = not used, `n` = in use.

### Trailer

- **Size:** Size of the document.
- **Root:** Root of the document structure.
- **Info:** Information about the document.
- **Start Xref:** Points to the xref table.
    
    ---
    

# EXE 

## Header

- **Import:** Can include code or functions from another file.
- **Export:** The functions within the EXE file that other files can call.
- **Timestamp:** Indicates the first compiler date.

## Sections

- **Subsystem:** Whether the EXE is for command line or GUI.
- **Resource:** Contains EXE menu, icon, image, font, etc.
- **Body:** Divided into segments (text, rdata, data, rsrc, reloc).

### Body

- **Text:** Holds PE EXE code.
- **Rdata:** Holds information about import (stored in idata) and export (edata) code.
- **Rsrc:** External resources used by the PE (icon, translation language, etc.)
- **Pdata:** Exception handling information.

**🟡Note:** If the memory size differs from the disk, it indicates a packer.

## EXE Analyzing Techniques

- **Static:** Analyzing without executing the file.
- **Dynamic:** Analyzing while the file is running.
- **Analyze Packer:** Checking for packed executables.
    
    ---
    

# Tools

## PDF

- **[pdfid](https://www.kali.org/tools/pdfid/):** Identifies PDF file characteristics.

## Microsoft

- **[oletool](https://github.com/decalage2/oletools):** Analyzes Microsoft Office Files.

## EXE

- **[Dependency Walker](https://dependencywalker.com/):** Analyzes dependencies of executables.
- **[peview](https://cybersectools.com/tools/peview):** Displays the header and sections of PE files.
- **[Hacker Resources](https://www.angusj.com/resourcehacker/):** Various tools and resources for analyzing executables.

