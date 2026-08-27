# Broken Internal Links — rst2md_converter output_md/source

Generated from `validate_internal_links()` against the current `output_md/source` build. Total: 20 issues, all `missing_target_file` — `missing_anchor` is now 0.

History: started at ~2069 issues, reduced to 291 by fixing the anchor-stripping/refuri-normalization bugs, reduced to 111 by making section headings always emit real anchors and auto-fixing text-matched stale links, then to 0 missing_anchor after `python/7apply-anchor-review.py` applied the human-reviewed suggestions from `plans/anchor-suggestions.md` (27 links fixed to their real target, 33 links stripped to plain text since no trustworthy target existed).

The remaining 20 all point to other manuals never migrated into this `input_rst` tree (`API_References/`, `SamplesGuide/`, and a few standalone pages like `Faq.md`, `Overview_GettingStarted.md`, `Overview_UsageRights.md`, `Plugins_Introduction.md`, `JS_API_acrojspreface.md`) — not fixable without adding that content to this repo.

To regenerate this list, run from `rst2md_converter/`:

```python
import sys, types
from pathlib import Path
src = open('python/1rst2md.py', encoding='utf-8').read()
end = src.index('CONF_PY: Optional[Path]')
mod = types.ModuleType('bl')
mod.__dict__['__name__'] = 'bl'
mod.__dict__['__file__'] = str((Path.cwd() / 'python' / '1rst2md.py').resolve())
sys.modules['bl'] = mod
exec(compile(src[:end], 'python/1rst2md.py', 'exec'), mod.__dict__)
issues = mod.validate_internal_links(Path('output_md/source').resolve())
for i in issues:
    print(i.docname, i.kind, i.message)
```

## Checklist

### interapp/iac-api-dde-messages.md (1)

- [ ] **missing_target_file**: Missing target file: ./API_References/Acrobat_API_Reference/index.md

### jsapiref/doc.md (1)

- [ ] **missing_target_file**: Missing target file: JS_API_acrojspreface.md

### jsapiref/js-api-acrojs.md (1)

- [ ] **missing_target_file**: Missing target file: ./API_References/Acrobat_API_Reference/index.md

### overview/apxdevfaq.md (1)

- [ ] **missing_target_file**: Missing target file: Faq.md

### overview/index.md (1)

- [ ] **missing_target_file**: Missing target file: Overview_GettingStarted.md

### overview/overview-forms.md (1)

- [ ] **missing_target_file**: Missing target file: Overview_UsageRights.md

### pdfcreation/pdf-create-commonsettings.md (1)

- [ ] **missing_target_file**: Missing target file: ./API_References/Acrobat_API_Reference/index.md

### plugin/index.md (1)

- [ ] **missing_target_file**: Missing target file: Plugins_Introduction.md

### plugin/plugins-a3d-api.md (1)

- [ ] **missing_target_file**: Missing target file: ./API_References/PRCReference/3D_API_Reference/index.md

### plugin/plugins-creatingsimpleplug.md (2)

- [ ] **missing_target_file**: Missing target file: ../SamplesGuide/book/Samples_Tools.md
- [ ] **missing_target_file**: Missing target file: ./snippet/index.md
