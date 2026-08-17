# Security

This is a **documentation and study** repository. There is no production application to patch. The risk is **secrets and personal data** landing in git history.

## Do not commit

- `.env`, API keys, tokens, connection strings
- Real patient identifiers (UHID, ABHA, names, mobiles, reports)
- Real customer PAN, account numbers, claim IDs
- Internal BRDs, HIS exports, or meeting recordings from an employer
- Screenshots that show another person’s clinical or billing data

If you practise SQL or Excel, use files named `sample_` with fake IDs.

## If something sensitive was committed

1. Do not make it worse with a second “clean” commit that still leaves history.
2. Rotate any exposed key or password immediately.
3. Remove the file from git history (filter-repo / BFG) or delete the repo and start clean if it was never needed.
4. If health data was involved, treat it as an incident: tell the data owner / DPO. Do not discuss the payload in a public issue.

## Reporting

Open a **private** advisory if the GitHub repo has that feature enabled, or email the repo owner. Do not paste the secret into a public issue.

## Generative AI

Do not paste this repo’s client-style practice data *and* real PHI into a public chatbot. Use an approved enterprise tenant and redaction. See `14-AI-for-Business-Analysts` and `18-Health-Domain-Research/06-gen-ai-foundations-for-healthcare-ba.md`.
