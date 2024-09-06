# HugoPlantUMLRenderer



**Create a New Hugo Site:** Create a new Hugo site by running:

```bash
hugo new site my-hugo-site
cd my-hugo-site
```

**Start the Hugo Server:** Run the Hugo server to see your site:

```bash
hugo server
```
Visit `http://localhost:1313` to view your site.


**Create a Shortcode File:** In your Hugo project directory, navigate to `layouts/shortcode`s and create a file named `plantuml.html`.

```bash
mkdir -p layouts/shortcodes
touch layouts/shortcodes/plantuml.html
```

Add this code to `plantuml.html`


```html
<div class="plantuml-diagram">
    <textarea id="plantuml-code" style="display:none;">
    {{ .Inner }}
    </textarea>
    <img id="plantuml-image" src="" alt="PlantUML Diagram" />
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            function encodeHex(data) {
                return data.split('').map(function(c) {
                    return c.charCodeAt(0).toString(16).padStart(2, '0');
                }).join('');
            }

            function compressToPlantUML(hex) {
                return "http://www.plantuml.com/plantuml/img/" + "~h" + hex ;
            }

            const code = document.getElementById('plantuml-code').value;
            const hex = encodeHex(code);
            document.getElementById('plantuml-image').src = compressToPlantUML(hex);
        });
    </script>
</div>

```


**Create a New Markdown Document:** Generate a new Markdown file for your content:
```bash
hugo new posts/my-first-post.md
```

```markdown
---
title: "My First Post"
date: 2024-09-07T00:00:00Z
draft: false
---

Here is a PlantUML diagram:

{{< plantuml >}}
@startuml
Alice -> Bob: test
@enduml
{{< /plantuml >}}


```

**Final Result:**

![image](https://github.com/user-attachments/assets/23f2cfa7-8b72-4711-8547-c0b116bc7038)







