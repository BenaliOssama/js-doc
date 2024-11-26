### **Understanding Go Templates**

---

#### 1. **Introduction to Go Templates**

Go templates provide a way to generate dynamic content by embedding data into text or HTML. They are commonly used in web development to generate HTML pages or in tools that output structured text files. Templates in Go are part of the `text/template` (for plain text) and `html/template` (for HTML) packages.

---

#### 2. **Key Features of Go Templates**

1. **Data-Driven**: Templates bind data structures (e.g., structs, maps) to placeholders.
2. **Safe HTML Escaping**: `html/template` automatically escapes data to prevent injection attacks.
3. **Control Structures**: Support for loops, conditionals, and more.
4. **Extensible**: Define custom template functions for advanced functionality.

---

#### 3. **Creating and Parsing Templates**

1. **Simple Template**:
   ```go
   package main

   import (
       "os"
       "text/template"
   )

   func main() {
       tmpl := `Hello, {{.Name}}!`
       data := struct{ Name string }{Name: "Alice"}

       t, _ := template.New("example").Parse(tmpl)
       t.Execute(os.Stdout, data)
   }
   ```

   Output:
   ```
   Hello, Alice!
   ```

   - `{{.Name}}`: Accesses the `Name` field of the provided data.

2. **Parsing Template Files**:
   ```go
   t, _ := template.ParseFiles("template.tmpl")
   t.Execute(os.Stdout, data)
   ```

3. **Parsing Multiple Templates**:
   ```go
   t, _ := template.ParseFiles("header.tmpl", "body.tmpl", "footer.tmpl")
   t.ExecuteTemplate(os.Stdout, "body", data)
   ```

---

#### 4. **Common Template Syntax**

- **Data Placeholder**:
  ```go
  {{.FieldName}}  // Access struct fields
  {{.}}           // Access root data
  ```

- **Conditionals**:
  ```go
  {{if .Field}}Condition True{{else}}Condition False{{end}}
  ```

- **Loops**:
  ```go
  {{range .Items}}
    {{.}}  // Iterates over a slice
  {{end}}
  ```

- **Function Calls**:
  ```go
  {{call .FuncName .Param}}
  ```

---

#### 5. **Template Functions**

Go templates include built-in functions (e.g., `len`, `print`) and allow you to define custom ones.

1. **Using Built-in Functions**:
   ```go
   {{len .Items}}  // Gets the length of a slice
   ```

2. **Custom Functions**:
   ```go
   func add(a, b int) int {
       return a + b
   }

   func main() {
       tmpl := `Sum: {{add .A .B}}`
       funcs := template.FuncMap{"add": add}

       t, _ := template.New("example").Funcs(funcs).Parse(tmpl)
       data := map[string]int{"A": 5, "B": 10}
       t.Execute(os.Stdout, data)
   }
   ```

---

#### 6. **HTML Templates**

The `html/template` package builds on `text/template` and is specialized for generating safe HTML output.

1. **Escaping User Input**:
   ```go
   package main

   import (
       "html/template"
       "os"
   )

   func main() {
       tmpl := `Hello, {{.}}!`
       data := "<script>alert('XSS')</script>"

       t, _ := template.New("example").Parse(tmpl)
       t.Execute(os.Stdout, template.HTML(data))
   }
   ```

2. **Embedding HTML Files**:
   ```go
   t, _ := template.ParseFiles("index.html")
   t.Execute(os.Stdout, data)
   ```

---

#### 7. **Error Handling in Templates**

- Always check for errors when parsing or executing templates:
  ```go
  if err := t.Execute(os.Stdout, data); err != nil {
      log.Println("Error executing template:", err)
  }
  ```

---

#### 8. **Template Best Practices**

1. **Organize Template Files**:
   - Store templates in a directory (e.g., `/templates`) and load them dynamically:
     ```go
     t, err := template.ParseGlob("templates/*.tmpl")
     ```

2. **Use `html/template` for Web Applications**:
   - Ensures safe HTML output and prevents XSS attacks.

3. **Avoid Complex Logic in Templates**:
   - Keep templates clean; move business logic to Go code.

4. **Define Common Layouts**:
   - Use `ExecuteTemplate` to render templates with shared headers/footers.

5. **Test Templates**:
   - Ensure templates work with valid and edge-case data.

---

#### 9. **Conclusion**

Go templates provide a flexible and efficient way to generate text and HTML content. By mastering template syntax, understanding the distinction between `text/template` and `html/template`, and following best practices, you can effectively create dynamic and safe outputs in your Go applications.

--- 

This guide serves as an overview of Go templates, their usage, and best practices to get you started with generating structured content dynamically.