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

`gliner2_modal_demo.py` defines the app, installs from `requirements.txt`, loads the model in `@modal.enter()`, and exposes one remote method that returns structured JSON plus a classification. The entrypoint prints the result.

## Dependencies

Everything installs from `requirements.txt`:

- gliner2
- torch (>=2.0.0)
- transformers (>=4.51.3, <5.2.0)
- huggingface_hub (>=0.21.4)
- tqdm
- sentencepiece
- onnxruntime
- requests
- urllib3
- certifi
- charset-normalizer
- idna
- safetensors
- tokenizers
- filelock
- packaging

If the container is missing something at runtime, add it there and run again.

Later you might swap `SCHEMA` / `CLS` for your domain or expose `analyze` over HTTP using FastAPI etc. —  nothing here depends on that.
