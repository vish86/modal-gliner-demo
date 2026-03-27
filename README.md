# Modal + GLiNER2

I wanted something small that shows GLiNER2 doing real work (not just entity labels) and Modal doing the boring parts: image, remote run, load the model once. The script runs `extract_json` and `classify_text` on the same string so you can see two APIs without a giant schema.

You need Python 3.10+, a Modal account, and the CLI (`pip install modal`, then `modal setup`).

From this folder:

```bash
modal run gliner2_modal_demo.py
```

Custom text:

```bash
modal run gliner2_modal_demo.py --text "Your paragraph here."
```

`gliner2_modal_demo.py` defines the app, installs deps with `pip_install` on the image, loads the model in `@modal.enter()`, and exposes one remote method that returns structured JSON plus a classification. The entrypoint prints the result.

Dependencies are the package list passed to `pip_install` at the top of that file (gliner2, torch, transformers stack, HTTP stack, etc.). If something is missing at runtime, add it there and run again.

Later you might swap `SCHEMA` / `CLS` for your domain or expose `analyze` over HTTP using FastAPI etc. — nothing here depends on that.
