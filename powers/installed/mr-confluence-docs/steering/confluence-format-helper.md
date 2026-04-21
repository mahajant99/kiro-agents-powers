---
inclusion: auto
---

# Confluence Storage Format Helper

This guide helps convert markdown documentation to Confluence storage format (XHTML).

## Basic Conversions

### Headers
```markdown
# H1 → <h1>H1</h1>
## H2 → <h2>H2</h2>
### H3 → <h3>H3</h3>
```

### Text Formatting
```markdown
**bold** → <strong>bold</strong>
*italic* → <em>italic</em>
`code` → <code>code</code>
```

### Lists

**Unordered**:
```xml
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

**Ordered**:
```xml
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
</ol>
```

### Links
```xml
<a href="https://example.com">Link Text</a>
```

### Tables
```xml
<table>
  <tbody>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
    <tr>
      <td>Cell 1</td>
      <td>Cell 2</td>
    </tr>
  </tbody>
</table>
```

### Code Blocks
```xml
<ac:structured-macro ac:name="code">
  <ac:parameter ac:name="language">java</ac:parameter>
  <ac:plain-text-body><![CDATA[
public class Example {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
  ]]></ac:plain-text-body>
</ac:structured-macro>
```

### Info/Warning Panels
```xml
<ac:structured-macro ac:name="info">
  <ac:rich-text-body>
    <p>This is an info panel</p>
  </ac:rich-text-body>
</ac:structured-macro>

<ac:structured-macro ac:name="warning">
  <ac:rich-text-body>
    <p>This is a warning panel</p>
  </ac:rich-text-body>
</ac:structured-macro>
```

## Complete Example

**Markdown**:
```markdown
# Bug Fix: Login Timeout Issue

## Overview
- **MR**: !123
- **Author**: John Doe

## Problem
Users experiencing timeout on login.

## Solution
Increased connection timeout to 30s.
```

**Confluence XHTML**:
```xml
<h1>Bug Fix: Login Timeout Issue</h1>

<h2>Overview</h2>
<ul>
  <li><strong>MR</strong>: !123</li>
  <li><strong>Author</strong>: John Doe</li>
</ul>

<h2>Problem</h2>
<p>Users experiencing timeout on login.</p>

<h2>Solution</h2>
<p>Increased connection timeout to 30s.</p>
```
