# j-code-ext-template-1

A JCode **templates** extension: first-party project templates scaffolded
on-device by the embedded runtime. Installed through the
[JCode Marketplace](https://github.com/janrick123/j-code-marketplace).

```
extension.yaml                 # manifest (id, name, version, type: templates, template ids)
templates/
  empty/template.yaml
  aspnet-vite-react-ts/template.yaml
  react-app/template.yaml
  angular-aspnet/template.yaml
```

## Manifest (`extension.yaml`)

```yaml
id: jcode.templates
name: JCode Project Templates
version: 0.2.0
type: templates
templates: [empty, aspnet-vite-react-ts, react-app, angular-aspnet]
```

## `template.yaml` schema

```yaml
id: <stable id, matches the directory name>
name: <display name>
description: <one or two lines>
requires: [dotnet, nodejs]       # toolchain ids from the SDK catalog
recipe:                          # ordered steps run on-device at create time
  - label: <progress label>
    workdir: "{{hostStaging}}"   # optional cwd (placeholders resolved)
    run: <shell snippet>
```

Placeholders resolved before each step: `{{name}}` (sanitized project name),
`{{projectDir}}` (project root in the runtime), `{{hostStaging}}` (a fresh ext4
scratch dir, `$HOME/.jcode-staging/<name>`). An empty `recipe:` just creates the
folder (the `empty` template).
