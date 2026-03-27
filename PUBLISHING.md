# Publishing checklist

## 1) Confirm you are allowed to release
- Verify your IRB/data-use terms allow public release of **derived embeddings** (and labels if included).
- Ensure there are **no original filenames** or subject identifiers.

## 2) Recommended hosting option (easiest)
**Keep the git repo small** (README + metadata + splits + checksums), and publish the large `.npy` files as **Release assets**:

1. Create an empty GitHub repo (e.g., `als-ssl-fusion-embeddings`).
2. Commit and push everything except the large arrays:
   - Keep `metadata/`, `splits/`, `README.md`, `PUBLISHING.md`, `SHA256SUMS.txt`
   - Do not commit `embeddings/*/*.npy` unless you are using Git LFS
3. Create a GitHub Release and upload an archive containing:
   - `embeddings/` (all `.npy` matrices)

Users can verify the download using `SHA256SUMS.txt`.

## 3) Git LFS option
If you have enough LFS quota, you can store the `.npy` matrices in git using LFS:
```bash
git lfs install
git lfs track "embeddings/**/*.npy"
git add .gitattributes
git add embeddings
git commit -m "Add embedding matrices (LFS)"
git push
```

