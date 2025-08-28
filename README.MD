# YEX - YAML Extended (v1.0)

YEX, or **YAML Extended**, is a new, intelligent data format designed to be both simpler for newcomers and more powerful for experts. While it builds on the familiar YAML 1.2 syntax, it uses a dedicated parser to introduce new features like dynamic variables, logical commands, and a robust ruleset system.

This README provides a high-level overview of the core features of YEX/1.0.

---

### Core Principles

* **Human-Readable:** YEX maintains YAML's focus on easy-to-read, clean syntax.
* **Extensible:** The language can be "modded" with new features via custom rulesets.
* **Dynamic:** YEX documents are more than just static data; they can compute new values and execute logic.

---

### Key Features

#### `+page` Command
Instead of the standard `---` document separator, YEX introduces the `+page` command, which allows for built-in metadata such as a title and description.

```YEX
+page !llmsLazyload !noWrite
  number: 0
  name: YEX header
  description: |
    Official YEX/1.0 header...
````

#### Variables and Equations

YEX supports a dynamic variable system. Variables are defined on a special `Page -1` (for global scope) or at the top of any other page (for local scope). They can be used in equations, which are intelligently calculated by the parser.

  * **Global Variables** (`$global.entities.entityID.key`): Accessible from any page.
  * **Local Variables** (`$local.entities.entityID.key`): Accessible only on the page where they are defined.

<!-- end list -->

```yex
global:
  entities:
    VecPaws:
      $Epic Status$ = ($Epic Number$ * 10)
      $Epic Number$ = 10
```

#### Conditional Logic with `+if`

The `+if` and `+ifNot` commands allow for simple logical operations within the document, enabling dynamic behavior.

```yex
$Epic Percent$:
  +if $Epic Number$ == 10,
    set $Epic Percent$ = "100%"
```

#### `.yexr` Rulesets and Templates

The `.yexr` file format serves as the "ruleset" for YEX. It defines all commands, operators, and features. It also includes an extensive library of built-in templates, which can be used to create standardized data structures.

  * **Required Keys:** A key with an asterisk (`*`) at the end is mandatory and must be defined.
  * **Optional Keys:** If an optional key is left blank, the parser will fill it with a default value.

<!-- end list -->

```yex
+template:
  name: "LLM_WebLink"
  keys:
    title*:
      type: string
      required: true
    url*:
      type: string
      required: true
```
